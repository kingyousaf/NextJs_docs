# next_mastary_docs


## video 3 - Project Structure

### You will be given some basic folders to start of with lets exaplin each one

- Pages - This is where all your routes will live
- Public - This is where all assets will live like images etc
- Styles - This is where all your styles will live like css 

We also get files like 
- Next.config.js - This is the settings of your application
- .eslintrc.json - To spot wrong code

## video 4 - Routing Section Intro

In regular REACT you are not given a routing system so many people download external packages to do the work for them like 
REACT Router

#### What is a routing system ?

The ability to go to diffrent pages

### Routing in NEXT Js

It is all handled for us through the Folder Pages

## video 5 - Routing with Pages Folder

In Next Js if you create a file in the Pages folder then it will become a route that you can visit

##### For Example:

If we create a file named details.js in the pages folder then visit [localhost:3000/details](http://localhost:3000/details) It will be 
its own page

pages/details.js
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

#### What is a landing page
The page that the user will first see when coming to your website

#### Creating a landing page

In the Pages folder we are giving the ``` index.js ``` this is out landing page.

The name index is special as it becomes the route of the folder meaning the first

pages/index.js
```
import React from 'react'

const index = () => {
  return (
    <div>index</div>
  )
}

export default index
```

Visit [localhost:3000/](http://localhost:3000/)

Now you have the ability to create any route you want in Next Js just

- name a file how you want in the pages folder ending in ```.js```
- Make sure its a function that is ```export default ```
- And simply visit ```localhost:3000/nameOfFile ```


## video 6 - Nested Routes

### What is a nested route ?

A route inside of another route like ``` /details/person1 ```

### To make nexted routes 

 we first make a folder and then put files inside of those```pages/folder1/file1```

Then when we visit that page at ```/folder1/file1``` we will be presented with that page.

### Making folder by itself

If you make just a folder called ```pages/blog``` and try to visit /blog youll get an error

To solve this use a index file, mentioned beofre it becomes the route of the folder meaning first

so we get ```pages/blog/index``` then when we visit ```/blog``` we will get the index page


## video 7 - Dynamic Routes

### What is a dynamic route

#### A route wich url values change

instead of making files for ```product/product1 and product/product2 etc ``` we instead make a single file which
will take care of all these use cases for us.

### To make a dynamic route 

we wrap the file like ```products1``` in [] braces and rename it to

```[productNumber].js```

Now if we visit ```/product/anythingAfter``` we will just get the ```[productNumber].js``` page

Now we can use this page to chnage its content depedning on which product we are on 

### Accessing the dynamic value

to access the ```anythingAfter``` value we use the ```useRouter``` Hook given to us by Next Js.

With this we can retieve the ```query``` which is the dynamic part of the url

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



## video 8 - Nested Dynamic Routes

These are routes which are nested in each other

but there values change

for example ```/product/sweater/1``` and ```/product/hat/1``` here the secodn and third params change

to achomplish this 
- we make folder named ```product``` in pages
- then another folder named ```[catogry]``` 
- inside of it ```[productNumber]```


### retreiving the values for a nested route

Know that we can make dynamic nested routes we want to retieve the values for each nested route

we could use this to filter or chnage the product or layout fo the page by making api calls

do reteieve the nexted values use 

```
 const router = useRouter();
 const { catogry, productNumber } = router.query;
```
