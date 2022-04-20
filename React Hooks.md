## Life Cycle

-   New LifeCycle

![生命周期（新）](<https://gitee.com/Coder-jin/PicStore/raw/master/react%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E6%96%B0).png>)

-   Earlier LifeCycle

![生命周期（旧）](<https://gitee.com/Coder-jin/PicStore/raw/master/react%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E6%97%A7).png>)

## useState

> `useState` is a _Hook_ (we’ll talk about what this means in a moment). We call it inside a function component to add some local state to it. React will preserve this state between re-renders. `useState` returns a pair: the _current_ state value and a function that lets you update it. You can call this function from an event handler or somewhere else. It’s similar to `this.setState` in a class, except it doesn’t merge the old and new state together

```jsx
import React, { useState } from "react";

function Example() {
    // Declare a new state variable, which we'll call "count"
    const [count, setCount] = useState(0);

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
    );
}
```

## useEffect

> Tip
>
> If you’re familiar with React class lifecycle methods, you can think of `useEffect` Hook as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` combined.

```jsx
import React, { useState, useEffect } from "react";

function Example() {
    const [count, setCount] = useState(0);

    // Similar to componentDidMount and componentDidUpdate:
    useEffect(() => {
        // Update the document title using the browser API
        document.title = `You clicked ${count} times`;
    });

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
    );
}
```
