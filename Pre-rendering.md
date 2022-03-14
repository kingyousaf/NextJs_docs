# summary

- [Pre-rendering](#Pre-rendering)
- [Static Generation](#Static-Generation)
- [Static Generation with getInitalProps](#Static-Generation-with-getInitalProps)
- [Pages Vs Components](#Pages-Vs-Components)
- [Inpecting Static Generation Builds](#Inpecting-Static-Generation-Builds)
- [SSG with Dynamic Parameters](#SSG-with-Dynamic-Parameters)
- [Incremental Static Regeneration](#Incremental-Static-Regeneration)
- [getStaticProps fallback](#getStaticProps-fallback )
- [Master detail Pattern](#Master-detail-Pattern)


# Pre-rendering

## What is pre-rendering ?

- The page is built before being sent to the clinet
- Next js generates the ```HTML``` with all its data in advance and serves it to the client 
- served a hydrated page source with all its content

## benerfits of using pre-rendering

- improves performance 
- ```HTML``` already built and served
- Good SEO
- All pages are automaticaly pre-rendered

## comparing REACT AND NEXTJS

- REACT makes the client load the Javascript makiing the load slow
- REACT the page souce is empty
- REACT has bad SEO
- REACT has to get data when on client


# Static Generation

## What is static generation ?
- Is a method of pre-rendering where ```HTML``` pages are generated at build time
- Pre-rendered pages can be pushed to a ```CDN```, ```cached``` and served to clients across the globe ```imedialty```
- Static content is fast and better for ```SEO``` and ```indexed``` by the search engine
- Useing it with ```getStaticProps``` and ```getStaticPaths``` can make dynamic pages

## issues with static generation
- The build time is proportional to the ```N'th``` pages
- Once generated pages can have ```stale``` data
 ## How to use static generation for a page?
 - By defualt it happens to eah page made in NEXT js
 
 ## When to use it ?
 - Blog pages
 - eCommernce
 - product pages
 - etc

 # Static Generation with getInitalProps
 
 ## What is getInitalProps ?
 - A function made by next js 
 - Will only run if you define it in a page component 
 - ```Runs only on the server side```
 - You can directly write ```server side code inside of it``` like things done in ```Nodejs```
 - Any api keys put inside wont be shown
 - Any code wrote inside of it will not be shipped to the final bundle
 - it will run on every request
 
 ## How to use it ?
 - Inside of a page component we ```export a async function called getInitalProps```
 - This will then run at build time and``` hydrate``` the page with data before sending it to the client
 - It will then pass this ```data``` as ```props to the page```

## Extra information 
- You can use a context wich is passed through the the function
- This gives you access to the params object
- The params object allows you to retieve dynamic paths
- ``` const {params} = context ```
- You can pull dynamic values like the ```[postid]``` we makde with params.postid

 ### code:
 ```bash
 export async function getStaticProps() {
    
}
 ```
 - inside of here we can do any logic we want
 - from making api calls to fetching data and then hydrating the page before it is served to the client.
 ### code:
 ```bash
 import React from "react";

const user = ({ users }) => {
  return (
    <>
      {users.map((user) => (
        <h1>{user.name}</h1>
      ))}
    </>
  );
};

export default user;

export async function getStaticProps() {
  const res = await fetch("https://jsonplaceholder.typicode.com/users");
  const data = await res.json();
  return {
    props: {
      users: data,
    },
  };
}

 ```
 ## When to use it ?
 - When you want to fetch data or talk with an endpoint in and api

## structuring the function

### Begining 
- You can add any logic you want insid eof it that you want to run

### Return
- When returning you need to follow the convention of returning an object
- Then inside of the  props define as many things you want to return as a prop to the page
- Then accept this as props by the page itself 

# Pages Vs Components

### Pages:
- Pages give automatic routing
- Accss to functions like getStaticProps etc

### Components 
- Used as re-usable elements in an UI
- Don't have access to page functions


# Inpecting Static Generation Builds

### Building an application
- Inside of package Json use the command ```build```

- Delete the inital ```.next``` folder 

### Run
```bash
yarn build
```
- This then creates an ```optimized``` build of out project
- In the terminal it will show the information about the project


# SSG with Dynamic Parameters

## What is SSG with Dynamic Parameters?
- When the parameter chnages so you then build a stastic version of the page wirth its new data inside
- Like the [blog](#Example-structure-of-folder) example

## When to use SSG with Dynamic Parameters

- When you have a list of items and want to show diffrent pages for each dynamic item when clciked
- When you follow the [master detail pattern](#What-is-the-Mater-detail-Pattern?)

## How to use SSG with Dynamic Parameters 

## Code: 
```pages/blog/index.js```
```bash
import Link from "next/link";
import React from "react";

const index = ({posts}) => {
    return (
      <>
        <ul>
          {posts.map((post) => (
            <li key={post.userId}>
              <Link href={`/Posts/${post.id}`}>
                <a>{post.title}</a>
              </Link>
            </li>
          ))}
        </ul>
      </>
    );
};

export default index;

export async function getStaticProps() {
  const res = await fetch("https://jsonplaceholder.typicode.com/posts");
  const Posts = await res.json();
  return {
    props: {
      posts: Posts,
    },
  };
}

```

```pages.blog/[postid].js ```
```bash
import { useRouter } from "next/router";
import React from "react";

const PostId = ({ Post }) => {
  const router = useRouter();
  return <div>{Post.title} post</div>;
};

export default PostId;

export async function getStaticProps(ctx) {
  const { params } = ctx;
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${params.postid}`
  );
  const data = await res.json();
  return {
    props: {
      Post: data,
    },
  };
}

export async function getStaticPaths() {
  const res = await fetch("https://jsonplaceholder.typicode.com/posts");
  const data = await res.json();

  const paths = data.map((post) => {
    return {
      params: {
        postid: `${post.id}`,
      },
    };
  });
  return {
    paths: paths,
    fallback: false,
  };
}


```

# Master detail Pattern

## What is the Mater detail Pattern?
- It is pattern followed in the UI
- In the pattern you have a mater page to show all the content of items
- Then clicking on a item will take you to a page with that content
- Like a blog site

### Example structure of folder 
- Pages have a ```blog``` folder with its ```index.js``` to show all blogs
- User visits /blog and clicks blog
- Pages also has a ```[blogId].js``` file in```/blog```
- wich will show the content of that blog
- We could pre-render both of these pages


# getStaticProps fallback 

## What is the fallback ?
- A mandetory value that has to be added 
- Three possible values ```false``` ```true``` ```'blocking'```

## How to use it 
### fallback value = ```false```
- The paths returned from getStaticPaths will be rendred in HTML at build time
- Any path not returned will be directed to a ```404``` page

```bash
export async function getStaticPaths() {
  const res = await fetch("https://jsonplaceholder.typicode.com/posts");
  const data = await res.json();

  const paths = data.map((post) => {
    return {
      params: {
        postid: `${post.id}`,
      },
    };
  });
  return {
    paths: paths,
    fallback: false,
  };
}
```

### fallback value = ```true```
- Paths not made at build time will ```not``` show a ```404 Page```
- The server will then ```build``` it and then ```serve``` the page
- Paths not made will show a ```fallback``` version of the page on the first request to that path
- At build time showit might show a ```error``` because the ```id``` undefined
- Use this to build your ```main pages``` then when they click on other pages use fallback to ```build the page and then serve it```.

### Fixing the error 

This is placed in the dynamic page ```[postid]```
code:
```bash
import { useRouter } from "next/router";
  if (router.isFallback) {
    return <h1>Loading component for post</h1>
  }
```
- This will show the loading component then a newly generated page when you visit a new param

### Showing a 404 page ```fallabck = true```

- in your ```[postid]``` async function getStaticProps have a ```notFound```
- ```notFound``` if ```true``` will show ```404 page``` if the params are incorect

code:
```
if(!data.id){
 return {
 notFound: true,
 }
}
```

### fallback value = ```blocking```
- similar to fallback is set to true but wont show anything while the page is being generated
- Paths not generated at build time will not result in a ```404```
- Instead will build the page on the server and then serve it
- then requesting for the same page will be served the built page 


## When to use it ?

#### fallback value = ```false```
- sutiable for an application with a few paths
- 
#### fallback value = ```true```
 - if your app has a very large number of static pages
 - like a large eCommerce sites
 - Like build popular products and fallbacks for other products

### fallback value = ```blocking```
- on ```UX``` level some users perfer no loading screens and just being served a page
- It prevents any layout shifts
- Some ```crawlers ``` didnt support JavaScript
- The ```crawlers``` would see a loading page then the main page
- Reccomended to keep it to ```true``` fallback and just have the main pages served then build the rest




# Incremental Static Regeneration

## Example :

- 1.) download [JSON-server](https://www.npmjs.com/package/json-server)
```bash
 yarn add json-server
```
- 2.) Make a file named ```db.json```

```
{
  "products": [
    {
      "id": 1,
      "title": "Product 1",
      "price": 1000,
      "description": "description 1"
    },
    {
      "id": 2,
      "title": "Product 2",
      "price": 15000,
      "description": "description 2"
    },
    {
      "id": 3,
      "title": "Product 3",
      "price": 2000,
      "description": "description 3"
    }
  ]
}
```
- 3.) ```package.json``` add in the scripts
```
 "serve-json": "json-server --watch db.json --port 4000"
```

 - 4.) run this command 
 ```bash
 yarn serve-json
 ```
 
 - 5.) Go to [localhost:4000/products](http://localhost:4000/products)
 
 - 6.) Now make a folder ```products``` give that an ```index.js``` and a ```[ID]``` file
 ```products/index.js```
 ```
 import Link from "next/link";
import React from "react";

const index = ({ products }) => {
  return (
    <>
      <ul>
        {products.map((product) => (
          <li key={product.id}>
            <Link href={`/products/${product.id}`}>
              <a>{product.title}</a>
            </Link>
          </li>
        ))}
      </ul>
    </>
  );
};

export default index;

export async function getStaticProps() {
  const res = await fetch("http://localhost:4000/products");
  const Products = await res.json();
  return {
    props: {
      products: Products,
    },
  };
}

 ```
 
 ```products/[ID].js```
 ```
 import { useRouter } from "next/router";
import React from "react";

const PostId = ({ Product }) => {
  const router = useRouter();
  if (router.isFallback) {
    return <h1>Loading component</h1>;
  }
  return <div>{Product.title} post</div>;
};

export default PostId;

export async function getStaticPaths() {
  return {
    paths: [{ params: { ID: "1" } }],
    fallback: true
  };
}

export async function getStaticProps(ctx) {
  const { params } = ctx;
  const res = await fetch(`http://localhost:4000/products/${params.ID}`);
  const data = await res.json();
  return {
    props: {
      Product: data,
    },
  };
}

 ```
 
 ```
 props: {
      products: Products,
    },
    revalidate: 4,
  };
 ```
 
 updates the stale data
## What is it ?
- A alternative to regular ```SSR``` to improve page builds for dynamic pages
- use ```Json server ``` for mock data that chnages

## How to use it
- ``` revalidate: number, ```` set for a ```getStaticProps```

## When to use it 
- When you have data that changes 
