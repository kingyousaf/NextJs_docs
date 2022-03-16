# Api -

- You can write all your bussiness logic here and it wont be shiped to with the final bowser bundle
- You dont need other libarys to simply configure a restful api

# Summary
 - [creating an api](#Creating-an-api)
 - [API GET request](#API-GET-request)


# Creating an api
 # What is an api endpoint
 - A endpoint that you can interct with by ```fetching``` ```adding``` and ```deleting information from````
 - 
 # How to create an api endpoint 
 - Inside of ```pages``` the ```api``` folder holds all the apis
 - creating a file in ```api``` will then create an api endpoint

- It is where you can write any node or api code here 

Code:
```pages/api/hello````
- Visit /api/hello to get a resposne
```
export default function handler(req, res) {
  res.status(200).json({ name: 'John Doe' })
}

```
 
 # When to create an api endpoint 
 - When you have your own api and can simply put in next js 
 - Makes it more simplar less relicance on other libarys as its built in



# API GET request

## What is a API GET request
- fetching data froman api endppint

## How to make a API GET request

code : 
```/data/comments```
```
export const comments = [
  {
    id: 1,
    text: "comment 1",
  },
  {
    id: 2,
    text: "comment 2",
  },
  {
    id: 3,
    text: "comment 3",
  },
];

```

``` /api/comments/index ```

```
import { comments } from "../../../data/comments";

export default function handler(req,res) {
    res.status(200).json(comments)
}
```

 
 ``` pages/comments/index```
 
 ```
 import React, { useState } from "react";

const index = () => {
  const [comments, setComments] = useState([]);
  const fetchComments = async () => {
    const res = await fetch("/api/comments");
    const data = await res.json();
    setComments(data);
  };
  return (
    <div>
      comments get <button onClick={fetchComments}> get comments</button>
      {comments.map((comment) => (
        <h1>{comment.text}</h1>
      ))}
    </div>
  );
};

export default index;

 ```
