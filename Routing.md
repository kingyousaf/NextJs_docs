# Routing

Next js supports routing out of the box, it provides a routing system for both static and dynamic routes through the pages folder, any files and folders made in here will then become a route.

## Static routing

In the pages directory any file made will then become a route you can visit

## Creating a static routes

## Example 1

pages/details

Creating a file names details will then create a route for it.

So if you visit /details you will be presented with the page and its contents

## Example 2

pages/person/details

This will also follow folder that are placed inside of it

So making a folder and then a file will then create that route to that page

So /person/details

## Dynamic routing

Routes made dynamic will have diffrent urls depending on information passed to them.

These will not be hard coded but chnage depending on diffrent variables.

## creating dynamic routes

To create a dynamic route you need to have a specific file name structure

wrap the page you want to be dynamic in brackets

[]

Then put the name of the page in the brackets

```bash
[person].tsx
```

also work for folders as well

```bash
[car]/[person].tsx
```

or

## warning

The example here will follow what comes next as the cars folder is not dynamic but you can still make person dyanmic it will just be alsways cars/dynamicValues

```bash
cars/[person].tsx
```

## acessing dynamic routes through hard typeing

Now that you have created a dynamic page anything after the / will go here

so /perosn1234 will then go here if you where to hard type it.

So going to /car1/person1 will be presented with person page and a diffrent url path eac time you chnage the url path but keep the strucutre of /somthing/somthing2

# Next router

Know that we have created dynamic pages and routes we can do more with it with the useRouter hook provided by next.

## query

query is the dynamic part of the url if you want to access it.

```bash
router = useRouter()

//display in the ui
{router.query.person}
```

## navigating to pages dynamicly

to naviagate between pages use the next Link component

```bash
import Link from "next/Link"
```

The href will have the template of the page you want to route to
If they are dynamic make sure to include the []

```bash
<Link href="/[details]/[person]">
<a> Link</a>
</Link>

```

we need to provide href to each link to know where to go

## To prevent a full page reload

add as="" next to the href and if the pages are dynamic to make sure that you have [] in the file name

## ading dynamic values to go to dynamic pages

lets say we dont want to hard code or hard type the urls instead what if we terieve this information from an outside source

Here i will use an array of people

```
{/** Getting from an api endpoint */}
const people = [
  {
    v: 'car1',
    name: 'person1',
  },
  {
    v: 'car2',
    name: 'person2',
  },
]
```

```
 {/** No refresh then */}
      {people.map((person) => (
        <Link as={`/${person.v}/${person.name}`} href="/[vehicles]/[person]">
          <a>{person.name}</a>
        </Link>
      ))}

```

You dont't need to map what you could do is simply retieve the information and in the as="" string
iterplate it and add the values you want

But make sure that in the href you keep the correct template of the page you want to go to.


# Upadted version

## Now the files are case sensitive

So make sure when routing you have correct case

## Dynamic linking

Now you no longer need to have an as="" in the link tag.

```
<Link href="brazil/bruno"> Naviagte </Link>

```
Now if you dontt add as there still wont be a full page refresh

## Now you can ignore certain pages based on settings

if you have tests that dont want to become routes you cannow ignore pages based on some settings defined by you

in you next.config.js you can add a file naming structure to pick up thos pages and make them pages

in the mmodule export add 
```
pageExtenshions: ["page.tsx"]
```
so you can put anything in there and if you add that to the end of a file then it will become a route
