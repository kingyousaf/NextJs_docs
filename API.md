# Api 

# Summary
 - [creating an api](#Creating-an-api)


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
 
