# summary

- [Pre-rendering](#Pre-rendering)
- [Static Generation](#Static-Generation)
- [Static Generation with getInitalProps](#Static-Generation-with-getInitalProps)
- [Pages Vs Components](#Pages-Vs-Components)
- [Inpecting Static Generation Builds](#Inpecting-Static-Generation-Builds)
- [SSG with Dynamic Parameters](#SSG-with-Dynamic-Parameters)
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
 - A method of pre-rendering where the ```HTML``` is generated at build time
 - Also fills any data needed into the ```HTML``` before hand
 - ```HTML```generated in advance 
 - Recommended method
 - pages are cached by a CDN and served to the client instantly
 - Perfomance booster 
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
      posts: Posts.slice(0,3),
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
  return {
    paths: [
      {
        params: {
          postid: "1",
        },
      },
      {
        params: {
          postid: "2",
        },
      },
      {
        params: {
          postid: "3",
        },
      },
    ],
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


