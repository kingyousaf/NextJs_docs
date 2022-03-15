# summary
-[Client-side Data fetching](Client-side-Data-fetching)



# Client-side Data fetching

## What is it
- fetching data not on the server.

## When to use it 
- Example user dahsboard hidden behinde a login screen
- When ```SEO``` is of not importance for private pages
- When there is no need to pre-render the data

## How to use it 

- regualt fercth method in react

### ```code:```

```
import React, { useEffect, useState } from "react";

const clientSide = () => {
  const [isLoading, setIsLoading] = useState(true);
  const [dahsbaordData, setDashboardData] = useState(null);

  useEffect(() => {
    async function makeApiCall() {
      const res = await fetch("http://localhost:4000/dashbaord");
      const data = await res.json();
      setDashboardData(data);
      setIsLoading(false);
    }
    makeApiCall();
  }, []);

  if (isLoading) {
    return <h1>Loading</h1>;
  }
  return (
    <div>
      {dahsbaordData.map((data) => (
        <>
          <h1>Posts {data.posts}</h1>
          <h1>Likes {data.likes}</h1>
          <h1>Followers {data.followers}</h1>
        </>
      ))}
    </div>
  );
};

export default clientSide;

```
