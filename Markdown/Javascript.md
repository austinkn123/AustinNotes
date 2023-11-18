# JAVASCRIPT

- Single thread = does one thing at a time
- callstack = data structure that records where we are in the code
  - has to finish the function execution on call stack to move on because it is single thread
- setTimeout
  - part of browser not part of v8 (chrome) source
  - with a call stack that has setTimeout in the middle, setTimeout is moved out of stack to complete the time, the code runs rest of code after
    - when setTimeout it pushes function execution to task queue
    - event loops runs
      - EVENT LOOP ONLY PUTS FUNCTION BACK ON STACK IF STACK IS CLEAR
    - puts function back on stack and gets run

spread operator:

llows you to expand and copy the properties or elements of an object, array, or iterable into another object, array, or function call. It is commonly used for creating shallow copies, merging objects, and spreading elements in various contexts. Here's how the spread operator works:

1. **Array Spreading:**

   ```
   javascriptCopy code
   const numbers = [1, 2, 3];
   const newNumbers = [...numbers, 4, 5]; // Creates a new array [1, 2, 3, 4, 5]
   ```

2. **Object Spreading:**

   ```
   javascriptCopy code
   const person = { name: "John", age: 30 };
   const newPerson = { ...person, city: "New York" }; // Creates a new object { name: "John", age: 30, city: "New York" }
   ```

3. **Function Arguments:**

   ```
   javascriptCopy code
   function add(a, b, c) {
     return a + b + c;
   }
   
   const numbers = [1, 2, 3];
   const sum = add(...numbers); // Equivalent to add(1, 2, 3)
   ```

4. **Copying Arrays and Objects:**

   ```
   javascriptCopy code
   const originalArray = [1, 2, 3];
   const copiedArray = [...originalArray]; // Creates a shallow copy of the array
   
   const originalObject = { name: "Alice", age: 25 };
   const copiedObject = { ...originalObject }; // Creates a shallow copy of the object
   ```

5. **Adding Elements to Arrays:**

   ```
   javascriptCopy code
   const fruits = ["apple", "banana"];
   const newFruits = [...fruits, "orange", "grape"]; // Creates a new array ["apple", "banana", "orange", "grape"]
   ```

6. **Cloning Objects with Modifications:**

   ```
   javascriptCopy code
   const originalObject = { name: "Bob", age: 35 };
   const updatedObject = { ...originalObject, age: 36 }; // Creates a new object with age updated to 36
   ```

The spread operator creates shallow copies, which means that nested objects or arrays are still shared between the original and the copied object