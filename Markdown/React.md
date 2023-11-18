# Javascript React

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



## useCallback

saves a function by caching it (memoizing) so the function doesn’t get recreated again every render

- useCallback functions only get recreated when dependency array is updated
- If the dependencies haven't changed, React returns the stored function reference instead of creating a new one. This helps avoid unnecessary re-renders in components that receive this function as a prop.

## useMemo

- similar to useCallback but memoizes a value

## useRef

- 

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