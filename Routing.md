# next_mastary_docs

This is all the information i have learned from [
Codevolution](https://www.youtube.com/watch?v=GOdu5C8JzL8&list=PLC3y8-rFHvwgC9mj0qv972IO5DmD-H0ZH&index=14)
and his playlist on [NextJS](https://www.youtube.com/watch?v=GOdu5C8JzL8&list=PLC3y8-rFHvwgC9mj0qv972IO5DmD-H0ZH&index=14)

### I will be dividing each section to its respected video and giving eveything 
### that i have learned from it, you can use this for refrence or a source of learning.



## video 1 - introdcution

### why use Next js

- File base routing
- pre-rendering
- Good SEO
- API Routs
- Fullstack framework
- Supports css modules
- provides multiple auth providers


getting started with NextJs

## video 2 - Hello World

### To get started with building NextJs applications we need some pre-requisites

- Have [NodeJs](https://nodejs.org/en/) installed
- Have [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable) installed
- Have a text editor, [VsCode](https://code.visualstudio.com/download)

#### Now to actually build a NextJs application

So we need to follow these steps in order to build a application

- Open up VsCode
- Open up an empty folder inside of it 
- Open up the intergrated terminal
- Run the command 
```bash 
yarn create next-app ./ 
```
After downloading it run 
```bash
yarn dev
```
To run it on a developemnt server over at [localhost:3000](http://localhost:3000/)

### Now you all set up lets get to coding


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

```[productNumber]```
