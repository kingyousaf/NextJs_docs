# summary

- [Pre-rendering](#Pre-rendering)
- [Static Generation](#Static-Generation)
- [Static Generation with getInitalProps](# #Static-Generation-with-getInitalProps)


# Pre-rendering

## What is prendering ?

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
 
 ## How to use it ?
 
 ## When to use it ?
