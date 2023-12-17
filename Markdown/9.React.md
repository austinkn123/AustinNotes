# Javascript React



## Useful  Tips

- Components and Functions always start with a captial letter
- To make a function public, export the function
- Hooks can only be declared at the top level
  - not within other hooks or in returns
- 

# Structure:

index.html is the file that gets rendered on the screen which has a div id of ‘root’

index.js uses the index.html and starts the app with the index.html display

Bootstrap = easier to use but more higher level and less customizable

Tailwind = more low level but very customizable

class component = older way of making components

- includes built in methods such as ‘componentDidMount(), componentDidUpdate(), componentWillUnmount(), etc.
- needs to be rendered before returning
- has an instance of this.state

functional component = newer way to make components

- uses state hooks to maintain component instead of built in methods
- more lightweight and easier to manage by being modular
- does NOT have instance of this.state

# DOM

**DOM** - Document Object Model

- represents the HTML structure of the page
- Like a tree structure with html as nodes managed by the browser
- Document is the root node

**Virtual DOM** - Exact copy of DOM but in memory

- By using the virtual DOM, React can batch updates and optimize the rendering process, resulting in better performance compared to directly manipulating the real DOM.
- Used by React to efficiently update and render components before applying changes to the real DOM.

### How it works

- When using React, updates happen in the virtual DOM first.
- Then, the browser DOM and virtual DOM are diffed or compared to see if there are any updates made to virtual DOM that must be reflected or updated in the browser DOM
- Updates are made to the browser DOM where its needed to match the virtual DOM.

### **State**

- Data defined in a component

### **Props**

- data being passed down to another component

### **Lifting state**

- having data being shared between components by using a parent component

### **Controlled component:**

- Data is bound to state (the component)

### **Uncontrolled component:**

- Data is not bound to state (the component)
  - Uses useRef hook instead of state hook

### **Refs**

- Changing data by manipulating the actual dom and bypass the virtual dom

### **Keys**

- when iterating through a array you need a key identifier

### **Context**

- pass data from one component to another and can skip children (so data can be passed to grandchild and doesn’t have to go through child)
  - Props can only be passed down one level at a time

## html semantics

## fragments: **<></>**

- React Fragments are a feature in React that allow you to group multiple elements together without introducing an additional wrapper element in the DOM.
  - before, you had to wrap them in a single parent element, like a **`<div>`**. BUT, this extra wrapping element was often unnecessary and could impact the structure and styling of your components.
  - **React Fragments provide a solution to this problem by allowing you to group elements together without creating a new DOM element**
- Doesn’t add new node to the DOM like **`<div>`** does



# Hooks

## useMemo

- lets you cache the result of a calculation between re-renders 

  - similar to useCallback but memoizes a value
  - **Memoization** = is an optimization technique that involves memorizing the result of expensive function calls and returning the cached result when the same inputs occur again. This helps in avoiding unnecessary calculations and improving the performance of a React application.

- **TLDR**: Lets you compute a calculation once and not every re-render

- The basic syntax of `useMemo` is as follows:

  ```jsx
  const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
  ```

  Here's a breakdown of the key components:

  - The first argument to `useMemo` is a function that computes a value.
  - The second argument is an array of dependencies. If any of the dependencies change between renders, the memoized value will be recomputed.

  ### Example:

  ```jsx
  import React, { useState, useMemo } from 'react';
  
  function ExpensiveComponent({ data }) {
    const expensiveValue = useMemo(() => {
      // Some expensive computation based on the data
      return data.map(item => item * 2);
    }, [data]);
  
    return (
      <div>
        <p>Expensive Value: {expensiveValue.join(', ')}</p>
      </div>
    );
  }
  
  function App() {
    const [data, setData] = useState([1, 2, 3, 4]);
  
    return (
      <div>
        <ExpensiveComponent data={data} />
        <button onClick={() => setData(prevData => [...prevData, Math.random()])}>
          Add Random Number
        </button>
      </div>
    );
  }
  ```

  In this example:

  - The `ExpensiveComponent` takes an array of `data` as a prop.
  - The expensive computation is done inside the `useMemo` hook. This computation is only executed when the `data` prop changes.
  - The button adds a random number to the `data` array. Since `data` is a dependency of `useMemo`, the expensive computation is re-executed only when `data` changes.

  ### When to Use `useMemo`:

  - **Computations:** Use `useMemo` for expensive calculations or functions to avoid recalculating them on every render.
  - **Reference Equality:** Use `useMemo` when dealing with objects or functions to ensure that the reference identity is maintained between renders.
  - **Preventing Unnecessary Renders:** It's particularly useful in scenarios where the calculation of a value is computationally expensive, and you want to avoid unnecessary recalculations on every render.

## useCallback

saves a function by caching it (memoizing) so the function doesn’t get recreated again every render

- useCallback functions only get recreated when dependency array is updated

- If the dependencies haven't changed, React returns the stored function reference instead of creating a new one. This helps avoid unnecessary re-renders in components that receive this function as a prop.

- **TLDR:**: (Even though this summary is still kinda long) 

  - It's particularly helpful when passing callbacks to child components to prevent unnecessary re-renders.
  - When a function is wrapped with `useCallback`, React will memoize the function instance. This means that the memoized function will only change if one of its dependencies (specified in the dependency array) changes. This can be useful to optimize performance, especially in scenarios where a component re-renders frequently

- Here's the basic syntax of `useCallback`:

  ```jsx
  const memoizedCallback = useCallback(
    () => {
      // function body
    },
    [/* dependencies */]
  );
  ```

  Here's a breakdown of how it works:

  - The first argument is the function that you want to memoize.
  - The second argument is an array of dependencies. If any of these dependencies change, the memoized callback will be recreated.

  ### Example:

  ```jsx
  import React, { useState, useCallback } from 'react';
  
  function ChildComponent({ onClick }) {
    console.log('ChildComponent is rendering');
    return <button onClick={onClick}>Click me</button>;
  }
  
  function ParentComponent() {
    const [count, setCount] = useState(0);
  
    const handleClick = useCallback(() => {
      setCount(count + 1);
    }, [count]);
  
    return (
      <div>
        <p>Count: {count}</p>
        <ChildComponent onClick={handleClick} />
      </div>
    );
  }
  ```

  In this example:

  - `handleClick` is the callback function that increments the `count` state.
  - `handleClick` is wrapped with `useCallback`, and its dependency array includes `count`.
  - The `ChildComponent` receives the memoized `onClick` callback.

  ### When to Use `useCallback`:

  - **Preventing Unnecessary Renders:** If a callback is passed down to child components and that callback depends on some props or state, using `useCallback` can prevent unnecessary re-renders of those child components.
  - **Optimizing Performance:** It can be beneficial in scenarios where the callback is used as a dependency for other hooks or functions, and you want to ensure that its reference doesn't change frequently.

  ### Caveat:

  While `useCallback` can be useful for performance optimization in certain scenarios, it's essential to use it judiciously. Using it excessively or inappropriately can lead to more complex code and potentially hinder performance rather than improve it. As with any optimization, it's crucial to profile and test to ensure it provides the expected benefits.

## useRef

- lets you reference a value that’s not needed for rendering (persists across renders)

- **TLDR:** Lets you hold a reference to a element in the DOM

- ### Basic Usage:

  ```jsx
  import React, { useRef, useEffect } from 'react';
  
  function MyComponent() {
    // Create a ref object
    const myRef = useRef(null);
  
    useEffect(() => {
      // Access the current property to get the ref value
      console.log(myRef.current);
    }, []);
  
    return <div ref={myRef}>Hello, world!</div>;
  }
  ```

  In this example:

  - `useRef(null)` creates a ref object with an initial value of `null`.
  - `myRef.current` is initially `null`, but when the `div` is rendered, it becomes a reference to that `div` element.
  - The `useEffect` hook logs the value of `myRef.current` after the initial render.

  ### Use Case: Accessing and Modifying DOM Elements:

  ```jsx
  import React, { useRef, useEffect } from 'react';
  
  function AutoFocusInput() {
    const inputRef = useRef(null);
  
    useEffect(() => {
      // Focus on the input element when the component mounts
      inputRef.current.focus();
    }, []);
  
    return <input ref={inputRef} />;
  }
  ```

  Here, `inputRef.current` provides direct access to the underlying DOM element, allowing you to perform actions like focusing on the input.

  ### Use Case: Keeping Mutable Values Between Renders:

  ```jsx
  import React, { useRef, useState } from 'react';
  
  function Counter() {
    const count = useRef(0); // Mutable value stored in a ref
  
    const increment = () => {
      count.current += 1;
      console.log(count.current);
    };
  
    return (
      <div>
        <p>Count: {count.current}</p>
        <button onClick={increment}>Increment</button>
      </div>
    );
  }
  ```

  In this example, the value of `count` persists across renders. Because it's stored in a `ref`, the component won't re-render when `count` changes.

  ### Note:

  - Mutating `ref.current` doesn't cause a component re-render. It's a way to keep mutable values between renders without triggering a re-render.
  - If you need to store values that do trigger a re-render, you should use the `useState` hook.
  - `useRef` is commonly used for accessing and interacting with DOM elements, but it's a versatile tool for any scenario where you need to persist mutable values across renders without causing re-renders.

## useState

- 

## useEffect

- 

## useContext

- 

## useImperativeHandle

- 

# Libraries:

## Yup:

A npm package that sets up form validation requirements

## React Helmet:

used to manage the **`<head>`** section of your React application. It allows you to dynamically set metadata, such as the title, description, and other **`<meta>`** tags, for each individual page in your application. This is useful for improving SEO (Search Engine Optimization) and providing rich metadata for social media sharing. By using **`react-helmet`**, you can control the content of the **`<head>`** section based on the currently rendered component

## **react-hook-form**:

handles form state management and validation

### Hook: useForm

https://react-hook-form.com/docs/useform

- **FormState** = This object contains information about the entire form state. It helps you to keep on track with the user's interaction with your form application.

- **HandleSubmit** = This function will receive the form data if form validation is successful.

- Register

   = This method allows you to register an input or select element and apply validation rules to React Hook Form. Validation rules are all based on the HTML standard and also allow for custom validation methods.

  - By invoking the register function and supplying an input's name, you will receive the following methods:
  - onChange, onBlur, ref, name

## tanstack/react-query:

https://tanstack.com/query/v4/docs/react/reference/useQuery

### Hook: useQuery

allows you to fetch data from a specified data source, such as an API endpoint, by providing the URL or query parameters. It handles the fetching process and caches the data.

- Once data is fetched, it is stored in memory for subsequent requests. Cached data can be shared across different components, which reduces unnecessary network request
- Data will be read from the cache unless you make a new network request or refetch
- The hook manages loading states, errors, and the fetched data itself. It provides an object with properties like **`isLoading`**, **`isError`**, **`data`**, and **`error`** that you can use to handle different states in your UI
- React Query does *not* invoke the `queryFn` on every re-render, even with the default `staleTime` of zero. Your app can re-render for various reasons at any time, so fetching every time would be insane!
- Some reasons why your query is refetching
  - If you see a refetch that you are not expecting, it is likely because you just focused the window and React Query is doing a `refetchOnWindowFocus`
  - React Query will trigger a refetch whenever the `queryKey` changes because query key acts like a dependency array in `useEffect`

### Hook: useQueryClient

(The **`useQueryClient`** hook returns the current **`QueryClient`** instance.)

It is used to perform actions that involve the entire query cache and its management, rather than a specific query.

### Data: Fresh vs Stale

- **Fresh**: Data will always be read from the cache so no network request is gunna happen

- Stale

  : Still get data from the cache, but it might not reflect the most up to date version of data

  - Stale queries are refetched automatically in the background when:
    - New instances of the query mount
    - The window is refocused
    - The network is reconnected
    - The query is optionally configured with a refetch interval

### StaleTime vs CacheTime:

- StaleTime

  : Time where a query switches from fresh to stale

  - Default time: 0

- CacheTime

  : Time where inactive data is removed from cache (garbage collection time)

  - Default time: 5 minutes
  - Probably need another network request to get fresh updated data