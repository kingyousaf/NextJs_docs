 # Pre-rendering and client side data fetching
 
 # Summary 
 - [Project description](#Project-description)
 

# Project-description
- Page will show a list of events hppening around you
- SEO 
- Request time data fetching
- Server side rendering
- Client side data fetching to filter events
- Shallow routing for addign filters 

```
import React, { useState } from "react";
import { useRouter } from "next/router";

const events = ({ eventList }) => {
  const router = useRouter();
  const [events, setEvenets] = useState(eventList);
  const fetchSportsEvenets = async () => {
    const res = await fetch(`http://localhost:4000/events?category=sports`);
    const data = await res.json();
    setEvenets(data);
    router.push("/events?category=sports", undefined, { shallow: true });
  };
  return (
    <>
      <div>
        <ul>
          {events.map((item) => (
            <li key={item.id}>
              <h1>{item.title}</h1> <div>{item.description}</div>
              <div>{item.category}</div>
            </li>
          ))}
        </ul>
        <button onClick={fetchSportsEvenets}>filter by sports</button>
      </div>
    </>
  );
};

export default events;

export async function getServerSideProps(ctx) {
  const { query } = ctx;
  const { category } = query;
  const queryStrign = category ? "category=sports" : "";
  const res = await fetch(`http://localhost:4000/events?${queryStrign}`);
  const data = await res.json();
  return {
    props: {
      eventList: data,
    },
  };
}

```
