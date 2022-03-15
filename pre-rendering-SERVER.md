# Server side generation


 # Summary
 - [SSR exaplianed](#SSR-explained)
 - [SSR getServerSideProps](#getServerSideProps)
 - [SSR Dynamic params](#SSR-with-Dynamic-params)
 - [SSR getServerSideProps Context](#SSR-getServerSideProps-Context)
 

# SSR explained

  ## What is SSR
  - Pre-rendering where ```HTML``` built at ```request time```
  - ```HTML``` generated for ```every request```
  
  ## When to use it 
  - For a website ```similair to twitter```
  - Allows you to have upto-date information and good SEO
  - If you need to fetch data on ```request```
  - ```personalised data``` and good ```SEO``` 
  
  ## How to use it 
  - Export function ```getServerSideProps```

# getServerSideProps

 ## What is getServerSideProps
 - Runs only the ```server side```
 - The function will not run on the``` client```
 - Code you write here will not be sent to the final bundle for the browser
 - Can write server side code directly in this function
 - Like things tipicly done in ``` Node js```
 - Any code for server logic will not be bundled for browser
 
 
 ## How to use it 
 - Export the function 
```
import React from "react";

const index = ({ articales }) => {
  return (
    <>
      <div>
        {articales.map((articale) => (
          <>
            <h1 key={articale.title}>{articale.title}</h1>
            <h2>{articale.catgory}</h2>
          </>
        ))}
      </div>
    </>
  );
};

export default index;

export async function getServerSideProps() {
  const res = await fetch("http://localhost:4000/news");
  const data = await res.json();
  return {
    props: {
      articales: data,
    },
  };
}

```

  ## when to use it 
  - Only for pre-rendering and ```not client-side data fetching```
  - If you want to build a page ```on request time```



# SSR with Dynamic params

```[category.js]```
```
import React from "react";

const category = ({ artical, category }) => {
  return (
    <div>
      {category}{" "}
      <h1>
        {artical.map((art) => (
          <h1 key={art.title}>{art.title}</h1>
        ))}
      </h1>
    </div>
  );
};

export default category;

export async function getServerSideProps(ctx) {
  const { params } = ctx;
  const { category } = params;
  const res = await fetch(`http://localhost:4000/news?category=${category}`);
  const data = await res.json();
  return {
    props: {
      artical: data,
      category,
    },
  };
}

```

```news```
```
import Link from "next/link";
import React from "react";

const index = ({ articales }) => {
  return (
    <>
      <div>
        {articales.map((articale) => (
          <>
            <Link href={`/news/${articale.category}`}>
              <a>{articale.title}</a>
            </Link>
          </>
        ))}
      </div>
    </>
  );
};

export default index;

export async function getServerSideProps() {
  const res = await fetch("http://localhost:4000/news");
  const data = await res.json();
  return {
    props: {
      articales: data,
    },
  };
}

```




# SSR getServerSideProps Context 

## Objects access from the context
- The ```Request``` and ```Resposne```
- Simalr to express js
```
  const { params , req, res, query} = ctx;
```
 ## Req
 - ```HTTP``` incoming object

## Res
- ```HTTP``` response object

## query
- dynamic url string

### Use this for user cookies and any logic that use in express and node here 
