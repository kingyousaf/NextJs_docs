# Api -

- You can write all your bussiness logic here and it wont be shiped to with the final bowser bundle
- You dont need other libarys to simply configure a restful api

# Summary
 - [creating an api](#Creating-an-api)
 - [API GET request](#API-GET-request)
 - [API POST request](#API-POST-request)
 - [Dynamic API Routes](#Dynamic-API-Routes)
 - [DELETE requests](#DELETE-requests)
 - [CATCH ALL routes](#CATCH-ALL-routes)
 - [APIS and Pre rendering](#APIS-and-Pre-rendering)


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
 
 
 # API-POST-request
 
 ## What is a POST request
 - When you want to send information to an api endpoint
 
 ## How to make a POST request
 code: 
 
 ``` api/comments```
 
 ```
 import { comments } from "../../../data/comments";

export default function handler(req, res) {
  if (req.method === "GET") {
    res.status(200).json(comments);
  } else if (req.method === "POST") {
    const comment = req.body.userComment;
    const newComment = {
      id: Date.now(),
      text: comment,
    };
    comments.push(newComment);
    res.status(201).json(newComment);
  }
}
 ```
 
 
```pages/comments```

```
import React, { useState } from "react";

const index = () => {
  const [comments, setComments] = useState([]);
  const [userComment, setUserComment] = useState("");
  const fetchComments = async () => {
    const res = await fetch("/api/comments");
    const data = await res.json();
    setComments(data);
  };
  const submit = async (e) => {
    e.preventDefault();
    const response = await fetch("/api/comments", {
      method: "POST",
      body: JSON.stringify({ userComment }),
      headers: {
        "Content-Type": "application/json",
      },
    })
    const data = await response.json()
    console.log(data)
  };
  return (
    <div>
      comments get <button onClick={fetchComments}> get comments</button>
      {comments.map((comment) => (
        <h1>{comment.text}</h1>
      ))}
      <form onSubmit={submit}>
        <input
          type="text"
          placeholder="comment"
          value={userComment}
          onChange={(e) => setUserComment(e.target.value)}
        />
        <button type="submit">Submit comment</button>
      </form>
    </div>
  );
};

export default index;

```



# Dynamic API Routes

## What is a dynmaic api route
- Use it for delete requests and finding or filtering 

## How to make a dynmaic route

- make a ```[commentId].js``` in ```comments``` add
```
import { comments } from "../../../data/comments";

export default function handler(req, res) {
  const { commentId } = req.query;
  const comment = comments.find(
    (comment) => comment.id === parseInt(commentId)
  );
  res.status(200).json(comment);
}

```

## When to make a dynmaic route
- For the example above to delete a specific comment by going to /commments/dynamciID then deleteing that


# DELETE requests
- Use the ame logic as in the above example 

## How to make a delete request

``` [commentsId].js```
```
import { comments } from "../../../data/comments";

export default function handler(req, res) {
  const { commentId } = req.query;
  if (req.method === "GET") {
    const comment = comments.find(
      (comment) => comment.id === parseInt(commentId)
    );
    res.status(200).json(comment);
  } else if (req.method === "DELETE") {
    const deletedComment = comments.find(
      (comment) => comment.id === parseInt(commentId)
    );
    const index = comments.findIndex(
      (comment) => comment.id === parseInt(commentId)
    );
    comments.splice(index, 1);
    res.status(200).json(deletedComment);
  }
}

```

``` pages/comments``` method on the button for each comment

```
 import React, { useState } from "react";

const index = () => {
  const [comments, setComments] = useState([]);
  const [userComment, setUserComment] = useState("");
  const fetchComments = async () => {
    const res = await fetch("/api/comments");
    const data = await res.json();
    setComments(data);
  };
  const submit = async (e) => {
    e.preventDefault();
    const response = await fetch("/api/comments", {
      method: "POST",
      body: JSON.stringify({ userComment }),
      headers: {
        "Content-Type": "application/json",
      },
    });
    const data = await response.json();
    console.log(data);
  };
  const deleteComment = async (commentId) => {
    const res = await fetch(`/api/comments/${commentId}`, {
      method: "DELETE",
    })
    const data = await res.json();
    console.log(data)
    fetchComments()
  };
  return (
    <div>
      comments get <button onClick={fetchComments}> get comments</button>
      {comments.map((comment) => (
        <>
          <h1>{comment.text}</h1>
          <button onClick={() => deleteComment(comment.id)}>
            delete comment
          </button>
        </>
      ))}
      <form onSubmit={submit}>
        <input
          type="text"
          placeholder="comment"
          value={userComment}
          onChange={(e) => setUserComment(e.target.value)}
        />
        <button type="submit">Submit comment</button>
      </form>
    </div>
  );
};

export default index;

```




# CATCH ALL routes

## What is a catch all api route
- For optional routes 
- For one route to handle a single function or a adional 100 optional 

## How to use a catch all route

- make the file name ```[...params].js```

```
export default function handler(req,res) {
    const params = req.query.params
    res.status(200).json(params);
    console.log(params)
}
```

example output ```["jejje","ejej"]``` etc ```http://localhost:3000/api/jejje/ejej```

## When to use a catch all route
- For a single route then having a bunch of more optional api routes


# APIS and Pre rendering
