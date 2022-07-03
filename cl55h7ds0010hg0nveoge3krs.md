## Automatic Batching in React 18

 **Batching** is when React groups multiple state updates into a single re-render for better performance. In React 17 and prior, updates inside React event handlers were batched. But updates inside of promises, setTimeout, native event handlers, or any other event were not batched in React by default. 
<br/>
  However, In **React18** we are introduced to improved version of batching called **Automatic Batching**. It will enabled batching of all the state updates regardless of where they are called.

Let us break out this batching process React 17 and prior along with React 18 and understand the problems we faced earlier.

## Problem with React 17 and Prior

  Before looking into the issue, let us understand how batching works in React 17 and prior version. Our app contains two states to manage user name and city. **onLoadUser** function will be invoked on button click.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656851029326/JXsPhmIHT.png align="left")

You can try the app in this @ [StackBlitz](https://stackblitz.com/edit/react-ve7run?file=src%2FuserInfo.js,src%2FApp.js) . Click on a button and you will see console statement each time our App re-renders.

If you observe the browser console, you will see that state changed message is logged only once for both state updates. (PS: Initial log statement occurs when your app gets mounted for the very first time).

```
import React, { useState, useEffect } from 'react';

export default function App() {
  const [name, setName] = useState();
  const [city, setCity] = useState();

  // Sync Function call
  const onLoadUser = () => {
    setName('Rahul');
    setCity('Bangalore');
  };

  useEffect(() => {
    console.log(`UseEffect Called: userDeatils ${name} ${city}`);
  }, [name, city]);

  return (
    <div>
      <h1>Print User details</h1>
      <p>
        User Name: <strong>{name}</strong>
      </p>
      <p>
        City: <strong>{city}</strong>
      </p>
      <button onClick={onLoadUser}>Fetch user details</button>
    </div>
  );
}
``` 
Now you have seen that React batched both state updates and re-rendered the component only once.
But, what if we execute state updates in a context that is not associated with the browser?

For example, consider a fetch() call that asynchronously loads data:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656856787455/IHd4dwoGI.png align="left")
 
If you observe the browser console after executing this example, you will see 2 messages. This indicates that two separate re-renders occur for each state update.

A fake API been used to fetch user details.

```
  const onLoadUser = () => {
    fetch('https://jsonplaceholder.typicode.com/users/1')
      .then((res) => res.json())
      .then((data) => {
        setName(data.name);
        setCity(data.address.city);
      });
  };
``` 
## Any drawback here?

As observed. we see two different behaviors with synchronous and asynchronous functions . It is a performance bottleneck. If there are lot of states coming in and you are re-rendering fairly heavy there can be multiple re-renders.
That’s why React introduced **Automatic Batching**.

## How Batching works in React18?

React v18 ensures that state updates invoked from any location will be batched by default. This will batch state updates, including native event handlers, asynchronous operations, timeouts, and intervals.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656857421334/qfbtbKzOe.png align="left")
> React version should be 18

If you observe the browser console after executing this example, you will see two messages. This indicates that only one re-render occurs as React batches all state updates regardless of where they are called.

## Conclusion

To sum up that react 18 will batch the state updates for us no matter if it is in a simple function containing multiple state updates or a web API and interfaces like setTimeout, fetch or a promise containing multiple state updates.

To know more about Automatic batching, check out [Discussions here](https://github.com/reactwg/react-18/discussions/21)

I write about the web; you can follow me on [Twitter](https://twitter.com/deraowl). If you liked the post, give some ❤️!! Cheers