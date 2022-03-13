# summary

- [Pre-rendering](#Pre-rendering)
- [Static Generation](#Static-Generation)
- [Static Generation with getInitalProps](#Static-Generation-with-getInitalProps)
- [Pages Vs Components](#Pages-Vs-Components)


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
 
 ## How to use it ?
 - Inside of a page component we ```export a async function called getInitalProps```
 - This will then run at build time and``` hydrate``` the page with data before sending it to the client
 - It will then pass this ```data``` as ```props to the page```

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
