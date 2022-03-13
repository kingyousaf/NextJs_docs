
# video 3 - Project Structure

### You will be given some basic folders to start of with lets explain each one

- Pages - This is where all your routes will live
- Public - This is where all assets will live like images etc
- Styles - This is where all your styles will live like css 

We also get files like 
- Next.config.js - This is the settings of your application
- .eslintrc.json - To spot wrong code

# video 4 - Routing Section Intro

In REACT you are not given a routing system so a external packages is downloaded

#### What is a routing system ?

The ability to go to diffrent pages

### Routing in NEXT Js

Pre-built in with the pages folder

# video 5 - Routing with Pages Folder

In the ```pages``` folder creating a file will make that route available

##### For Example:

create :
- ```details.js``` in ```Pages```
- visit [localhost:3000/details](http://localhost:3000/details) 
- Add any specific content to that page

Code:
```pages/details.js```
```bash
import React from 'react'

const details = () => {
  return (
    <div>details</div>
  )
}

export default details
```
#### Rules to follow when creating a page
- All files must be a exported default for next js to pick them up

### How to create a landing page

#### What is a landing page ?
The page that the user will first see when coming to your website

#### Creating a landing page

To create a landing page:
- ```Pages``` file ```index.js``` is your landing page
- Visit [localhost:3000/](http://localhost:3000/)
- The name ```index.js``` will make it the defualt route for that folder

Code:
```pages/index.js```
```
import React from 'react'

const index = () => {
  return (
    <div>index</div>
  )
}

export default index
```

#### Now you have the ability to create any route you want in Next Js just

- name a file how you want in the ```pages``` folder
- Make sure its a function that is ```export default ```
- And simply visit ```localhost:3000/nameOfFile ```


# video 6 - Nested Routes

### What is a nested route ?

A route inside of another route like ``` /details/person1 ```

### To make nexted routes:

- make a folder named ```nested``` in ```pages```
- inside of ```nested``` make a file named ```route1```
- Visit [localhost:3000](https://localhost:300/nested/route1


### Visting a folder route by itself

- You made a folder named ```nested```
- You want to visit ```/nested``` by itself
- Add a ```index.js``` file inside of it
- This will show when visiting ```/nested```


# video 7 - Dynamic Routes

### What is a dynamic route?

#### A url which values chnage

```/blog/1``` and ```/blog/2``` etc

### How to make a dynamic routes:

- wrap the file in ```[ ]```braces 
- Example ```[blogNumber].js``` in ```pages/blog/[blogNumber].js```
- Visit [localhost:3000/blog/1](https://localhost:3000/blog/1) and [localhost:3000/blog/1](https://localhost:3000/blog/2)
- There ```url``` params are diffrent but they serve the same page

#### When to use dynamic pages

- serve the same page layout but put diffrent content in them based on the ```url``` params

### Changing the content in a dynamic page

- First we need to get the dynamic ```url``` values like ```/blog/1``` the ```1```
- To retreieve the ```1``` we use ```Next Router```
- The dynamic bit of the ```url``` is called a ```query```
- To access the query we use this code:
```
import { useRouter } from 'next/router'
import React from 'react'

const ProductNumber = () => {
  const router = useRouter()
  console.log(router.query.ProductNumber);
  return <div>ProductNumber</div>;
}

export default ProductNumber;
```
- The we can do multiple stuff like call an api with the params of the url to show specific content etc


# video 8 - Nested Dynamic Routes

### What is a nested Dynamic Route?

- It is like a regular nested route but there are more variables that can change
- Like ```product/sweater/1``` and ```/product/hat/1```
- The second and third params change and they are ```nested``` in ```product```

### How to make nested Dynamic Route

- Make a folder named ```product``` in ```pages```
- inside of ```product``` make another folder named ```[typeOfProduct]```
- inside of ```[typeOfProduct]``` make a file named ```[productId].js```
- Now we have ```pages/[typeOfProduct]/[productId].js```
- If we then put two ```/``` after product with params we will be served the single page
- We can continue the nesting as much as you want

### retreiving the values for a nested route

- use ```Next Router ``` like for single dynamic pages
- Pull the dynamic values from the url 
code:
```
 const router = useRouter();
 const { typeOfProduct, productId } = router.query;
```
From here you can make diffrent api calls or change the content accordingly with the information

# video 9 - Catch All Routes

### What is a catch all route ?

- a route that you will be taken to regardless of nesting
- Lests say we want to show the same page after every dynamic param after ```/docs```

### How to make a catch all route

- Inside of ```docs``` folder make a file named ```[...params].js```
- You need to have the convention of ```[...nameOfFile].js``` for it to work
- Youll have ```pages/docs/[...params].js```
- Now if you visit anything after ```/docs``` youll get served this page
- Like ```/docs/example/2/third``` every dynamic value after will still be served this page
- But from here you csn change the content by filltering for example


### How to make a defualt catch route
 if you want to show a route regarless of any none specified route if a person visits then wrap the ```[...params].js``` in another ```[ ]```
 
 Like ```[[...params]].js```
 
 This will be showed then.
 
 # video 10 - Link Component Navigation
 
 ### What is a Link component 
 - A compoennt provided by Next js
 - Used to navaigate between pages
 - Prevents refresh of the page
 - Allow users to be dynamicly taken to diffrent pages

 ### How to use a link component
 code:
 ```bash
 import Link from 'next/link'
 
 <Link href="/somewhere">
     <a>go to blog</a>
  </Link>
 ```
 - Wrapp the item you want to naviagte a person
 - give it a hard typed route like ```/details``` or 
 - dynamicly put the route in with string interpealation

 ```bash
 href={`${details.catogry}/${productNumber}`}
 ```
 - These could be taken from an api call or a product thats clicked

 # video 11 - Navigating Programmatically
 
 ### What is Navigating Programmatically?
 - To make a user chnage his page by him making or a action happening

 ### How to Naviagte Programmatically
 - Use the ```useRouter``` hook
 - in some logic that you add example a click run a function
 - Push the user to a diffrent part of the page
 ```
  router.push("/details/completePage")
 ```

 # video 12 - Custom 404 Page

 ### What is a 404 page ?
 - A page shown when a user neters an invalide url

 ### How to create a Custom 404 Page
 - Make a file in ```pages``` called ```404.js```
 - Its like a simple page so add anything you want insid e of it
