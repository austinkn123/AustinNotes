# JAVASCRIPT

## General

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

## spread operator:

allows you to expand and copy the properties or elements of an object, array, or iterable into another object, array, or function call. It is commonly used for creating shallow copies, merging objects, and spreading elements in various contexts. Here's how the spread operator works:

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



## Tips and Tricks

- use `typeof` to see a variables type if you are unsure

- use ternary statements for shorthanded conditionals

  - ```javascript
    function getFee(isMember) {
      return isMember ? '$2.00' : '$10.00';
    }
    
    console.log(getFee(true));
    // Expected output: "$2.00"
    
    console.log(getFee(false));
    // Expected output: "$10.00"
    
    console.log(getFee(null));
    // Expected output: "$10.00"
    
    ```

    

- use `&&` for a ternary statement without the else

  - ```javascript
    x && y //returns whichever is true or not null
    ```

    

## This:

A keyword in JavaScript that refers to the current instance of an object

- the behavior of `this` depends on how a function is being called

### Examples

1. **Global Context:**

   - In the global context (outside of any function or object), `this` refers to the global object. In a browser environment, the global object is `window`.

   ```javascript
   console.log(this); // points to the global object (e.g., window in a browser)
   ```

2. **Function Context:**

   - Inside a function, the value of `this` depends on how the function is called.
   - When a function is called as a standalone function (not as a method of an object), `this` still refers to the global object (or `undefined` in strict mode).

   ```javascript
   function myFunction() {
     console.log(this);
   }
   
   myFunction(); // points to the global object (e.g., window in a browser)
   ```

3. **Method Context:**

   - When a function is a method of an object, `this` refers to the object on which the method is called.

   ```javascript
   var obj = {
     myMethod: function() {
       console.log(this);
     }
   };
   
   obj.myMethod(); // points to the 'obj' object
   ```

4. **Constructor Context:**

   - When a function is used as a constructor with the `new` keyword, `this` refers to the newly created instance of the object.

   ```javascript
   function MyClass() {
     console.log(this);
   }
   
   var myInstance = new MyClass(); // points to the newly created instance
   ```

5. **Event Handlers:**

   - In event handlers, the value of `this` depends on the context in which the handler is called. It may not always be the object that triggered the event.

   ```javascript
   var button = document.getElementById('myButton');
   
   button.addEventListener('click', function() {
     console.log(this); // points to the 'button' element
   });
   ```

6. **Arrow Functions:**

   - Arrow functions do not have their own `this`. They inherit `this` from the enclosing lexical scope. This is different from regular functions that have their own `this`.

   ```javascript
   var obj = {
     myMethod: function() {
       setTimeout(() => {
         console.log(this); // points to the 'obj' object
       }, 1000);
     }
   };
   
   obj.myMethod();
   ```



## DOM Manipulation

### More In-depth Explaination: 

https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction

the DOM (**Document Object Model**) is a tree-like representation of the contents of a webpage

the DOM is a tree of **nodes**

when your HTML code is parsed by a web browser - it is converted to a DOM 

the nodes are objects that have many properties and methods attached to them

these properties and methods are the primary tools we use to manipulate our webpage with JavaScript



### DOM Selectors

to target DOM nodes we use the `querySelector()` method

```javascript
element.querySelector(selector) // returns a reference to the first match for 'selector'

element.querySelectorAll(selector) // returns a "nodelist" w references to all the matches for 'selector'
```

note `element` here can really be any element/node - but most often the `document` object is used 

note the "nodelist" is *not* an array - it is a "nodelist" and does not have all the same methods available to arrays

you can, of course, convert a nodelist to an array with `Array.from()`



for the actual **selector** there are two options..

```html
<div id="container">
  <div class="display"></div>
  <div class="controls"></div>
</div>
```

**CSS-style selectors**:

```javascript
div.display
.display
#container > .display
div#container > div.display
```

or

**Relational selectors**:

```javascript
const container = document.querySelector('#container');
container.firstElementChild; // selects .display
const controls = document.querySelector('.controls');
controls.previousElementSibling; // selects .display

somediv.firstElementChild
somediv.lastElementChild
somediv.nextElementSibling
somediv.previousElementSibling
...
```



**Create Element**

```javascript
document.createElement(tagName, [options]); // create new element with tag-type tagName

const newDiv = document.createElement('div');
```

*note the above does not add the new element to the DOM - it simply creates it in memory

you can manipulate the element (add styles, classes, text, etc) before placing it on the page

you place the element on the page with the append method (below)



**Append Element**

```javascript
parentNode.appendChild(childNode); // append childNode as the last child of parentNode

body.appendChild(newDiv);
```

```javascript
parentNode.insertBefore(newNode, referenceNode); // inserts newNode into parentNode before referenceNode

body.insertBefore(newDiv, btn)
```



**Remove Element**

```javascript
parentNode.removeChild(child); // removes child from parentNode and returns a reference to child
```



**Altering Elements**

```javascript
const newDiv = document.createElement('div');                     
// creates a new div referenced by the variable 'newDiv'

newDiv.style.color = 'blue';                                      
// add the indicated style rule

newDiv.style.cssText = 'color: blue; background-color: white;';          
// add several style rules - any previous styles set with javascript will be overwritten

newDiv.setAttribute('style', 'color: blue; background-color: white;');    
// add several style rules - any previous styles set with javascript will be overwritten
```

note we can **get** the current style with..

```javascript
console.log(newDiv.style.color); // 'blue' - only works for styles previously set with javascript
```

and **remove** the current style with..

```javascript
newDiv.style.color = ''; // only afects styles previously set with javavascript
```



**Editing Attributes**

```javascript
newDiv.setAttribute('id', 'coolDiv'); // note these are html element attributes like id, class, src,
									  // style, href, etc

newDiv.getAttribute('id'); // "coolDiv"

newDiv.removeAttribute('id');
```



**CSS Classes**

```javascript
newDiv.classList.add('new');                                      
// adds class "new" to newDiv

newDiv.classList.remove('new');                                   
// removes class "new" from newDiv

newDiv.classList.toggle('make-blue');                                
// if newDiv doesn't have class "make-blue" then add it, or if
// it does, remove it

newDiv.classList.add('sup', 'cool', 'fun'); // syntax for multiple entries
```

*it is best practice and usually cleaner to use a CSS class rather than adding/removing inline CSS



**Adding Text and HTML Content**

```javascript
newDiv.textContent = 'Hello World!';

newDiv.innerHTML = '<span>Hello World!</span>';
```

you should use `textContent` to edit text

and use `innerHTML` to edit HTML  - note that `innerHTML` poses a security risk!

if you use `innerHTML` make sure nothing that goes into that innerHTML is written/sent by the user [LINK](https://www.youtube.com/watch?v=ns1LX6mEvyM)



note there is also `innerText` which approximates the text the user would get from the UI if they highlighted the contents of the element with the cursor and copied it



## Chrome DevTools Debugging

### DOM nodes

to access DOM nodes (elements) from the Console or referencing them with JavaScript..

- the currently-selected node can be referenced in the Console with the variable `$0`
- as if.. `let $0 = (currently selected node);` has occured



alternatively you can store a node as a global variable (for more frequent use)..

- right-click the node in the DOM tree --> Store as global variable
- DevTools will create variable `temp1` to store the node.. and `temp2.. temp3.. etc` for subsequent global variables



you can copy the JavaScript path of a DOM node by right-clicking on the node --> Copy JS path

a `document.querySelector()` expression that resolves to the node is copied



### Breakpoints

The **Sources** panel is where you debug JavaScript in DevTools - in the Sources panel > open the js file you want to debug



While paused on the breakpoint..

- DevTools will print (next to each line of code) relevant variable values
- the **Scope pane** shows what local and global variables are currently defined
- the **Call Stack pane** shows the call stack



While paused on a breakpoint..

The **Watch Expressions pane** allows you to monitor variable and/or expression values over time - for example you could add.. `typeof userName` to watch the data type of variable `userName`

You can also just **use the Console** to test things out, like manipulate variables, while paused on a breakpoint



**edit JavaScript** directly in the Sources panel - use `Ctrl S` to save changes - of course it resets if you refresh the page



[Breakpoint Types](https://developer.chrome.com/docs/devtools/javascript/breakpoints/)

- Line-of-code
- Conditional Line-of-code
- DOM
- XHR
- Event Listener
- Exception
- Function



**Line-of-code breakpoint** - the most common type of breakpoint - will pause **before** the specified line is executed

in the js file (Sources panel) > click on the line number you want to break on (it turns blue)

You can also add `debugger;` directly to your source code - this is equivalent to a Line-of-code breakpoint

```javascript
x = "12";
debugger;
x = +x;
```



**Conditional Line-of-code breakpoint** - when you know the region of code that you want to investigate, but you want to pause only when some condition is true

in the js file > right-click on the line number you want to break on > Add conditional breakpoint > enter your condition (it turns orange) for ex: `typeof userName === "string"`



**DOM breakpoint** - will pause when the js modifies DOM nodes

NOTE it does not seem to work well with DOM modification that occur on page load

but typically we are not modifying the DOM on page load

Note `body` does sometimes have script elements added to it on page load (for example Live Server or Honey scripts)

And this has crashed Chrome for me before :(

`right click` an element in the DOM > `Break on..` >

**subtree modifications** - triggered when a **child** of that node is added, removed, or the contents of a child is changed - not triggered by attribute changes

**attribute modifications** - triggered when **that node** has an **attribute** added, removed, or changed

**node removal** -  triggered when **that node** is removed



**XHR/Fetch breakpoint** - will pause when the request URL of an XHR contains a specified string - [huh?](https://developer.chrome.com/docs/devtools/javascript/breakpoints/#xhr)



**Event Listener Breakpoint** - will pause on the event listener code that runs after an event is fired

for example when a 'click' Event Listener is triggered..

in Sources > Event Listener Breakpoints > Mouse > click (check)



**Exception breakpoints** - will pause on the line of code that's throwing a caught or uncaught exception

in Sources > right panel > Breakpoints > Pause on caught or uncaught exceptions



**Function breakpoints** - [LINK](https://developer.chrome.com/docs/devtools/javascript/breakpoints/#function)



## Data Types

every value in javascript has a data type

there are many data types

javascript variables are not limited - they can hold any of the data types

and we can change a variable's data type at any moment

```javascript
let message = "hello";
message = 123456;
```

**programming languages** that allow such things, such as javascript, are said to be **dynamically typed**

**dynamically typed** means there exists data types - but variables are not bound to any of them

note doing math in javascript is "safe" meaning the script will never stop with a fatal error (die), at worst we'll get `NaN`



There are **8 basic data types** in **JavaScript**

- Seven **primitive** data types:
  - `number` for numbers of any kind: integer or floating-point, integers are limited by `±(2^53-1)`
  - `bigint` for integer numbers of arbitrary length
  - `string` for strings - a string may have zero or more characters
  - `boolean` for `true`/`false`
  - `null` for unknown values - a standalone type that has a single value `null`
  - `undefined` for undefined values - a standalone type that has a single value `undefined`
  - `symbol` for unique identifiers
- And one **non-primitive** data type:
  - `object` for more complex data structures

​	

### Number

```javascript
// TYPE 1 - Number - for integers and floating point numbers (also Infinity, -Infinity, and NaN)

let n = 123;
n = 12.345;
```

javascript has **only one** data type for **all numbers**.. both integers and floats are data type `number`

note in javascript the `number` data type does not accurately represent integer values outside of the range..

`-(2^53 - 1) to (2^53 - 1)` 

`-9007199254740991 to 9007199254740991` (note this is a 16 digit number)

outside of this range there will be precision errors

because only so many digits fit into the fixed 64-bit storage

and therefore an approximate value may be stored

--> avoid using **integers** larger than **15 digits** and you should be good

--> avoid using more than **16 digits** when a decimal is present

```javascript
let x = 123456789123456;   // 15 digits --> is ok
let y = 123456789123456.7;  // 16 digits with a decimal --> is ok
let y = 123456789.1234567;  // 16 digits with a decimal --> is ok
```



### BigInt

```javascript
// TYPE 2 - BigInt - was created to store larger integers!

// simply append 'n' at the end of a large integer
const bigNumber = 1234567890123456789012345678901234567890n;

bigNumber; // returns 1234567890123456789012345678901234567890n
typeof bigNumber; // returns bigint

```



### String

Note: a **method** is a bit of functionality that is built into the language or into specific data types

for example JavaScript **string methods** are a bunch of things you can do with strings

```javascript
// TYPE 3 - String - is surrounded by quotes

let str = "Hello"; // 'single' and "double" quotes have the same functionality in javascript
let str2 = 'Hello';
let phrase = `why ${str} how do you do?`; // backticks

// backticks can be thought of as 'extended functionality quotes' in javascript
// they allow you to embed variables and expressions within a string

let name = "John";
// embed a variable
alert(`Hello, ${name}!`); // Hello, John!
// embed an expression
alert(`the result is ${1 + 2}`); // the result is 3
```

**escaping characters** in a string..

```javascript
const singleQuotes = 'I\'ve got no time!' // use a backslash \ to escape special characters
const doubleQuotes = "They called me \"the turtle\" back then."
```

as we saw before, to join strings together (**concatenate**) in javascript we use a type of string called a **template literal**

which is just a string which uses backticks instead of quotes..

```javascript
const one = "Hello, ";
const two = "how are you?";
const joined = `${one}${two}`;
joined; // "Hello, how are you?"
```

you can also **concatenate** strings with `+`

```javascript
const greeting = "Hello";
const name = "Chris";
greeting + ", " + name; // "Hello, Chris"
```

but **template literals** usually give you more readable code..

```javascript
`${greeting}, ${name}`; // "Hello, Chris"
```

note **template literals** respect line breaks..

```javascript
const multipleLines = `I like this song.
It is very hip.`;

multipleLines; /* I like this song.
				  It is very hip. */
```

to generate the equivalent output using normal quotes you would have to include line break `\n` characters..

```javascript
const multipleLines = "I like this song.\nIt is very hip.";

multipleLines; /* I like this song.
				  It is very hip. */
```



### Boolean

```javascript
// TYPE 4 - Boolean (logical) - has only two values: true and false

/* user checks a checkbox */
let checkBoxChecked = true;
typeof checkBoxChecked; // returns boolean

4 > 1; // returns true (boolean)
```



### Null

```javascript
// TYPE 5 - Null - the value 'null' is the only value with data type 'null'

let age = null; // this is simply stating that age is unknown

// null simply represents "nothing", "empty", or "value unknown" - it's like a placeholder

typeof null; // returns 'object'

// which is an officially recognized error in typeof, coming from very early days of JavaScript and kept for compatibility - null is not an object - it's a special value with a separate type of its own - the behavior of typeof is wrong here
```



### Undefined

```javascript
// TYPE 6 - Undefined - the value 'undefined' is the only value with data type 'undefined'

let x;
x; // returns "undefined"
typeof x; // returns "undefined"

// undefined simply means "variable is not defined"
```



### Object

The **object** data type is used to store **collections** of data and more complex entities

- Different from an array by having key-value pairs

Nearly all objects in JavaScript are instances of `Object`; a typical object inherits properties (including methods) from Object.prototype (talked about later)



**All other** data types are called **primitive** because their values can contain only a **single thing** (string, number, expression, etc.)

```javascript
// TYPE 7 - Object 
const myObject = {
  property: 'Value!',
  otherProperty: 77,
  "obnoxious property": function() {
    // do stuff!
  }
};

// dot notation
myObject.property; // 'Value!'

// bracket notation
myObject["obnoxious property"]; // [Function]


const variable = 'property';

myObject[variable]; // this is equivalent to myObject['property'] and returns 'Value!'
```

#### Object Constructors:

If you want to use a specific object over and over again, a good way could be to make object constructors

```javascript
function Player(name, marker) {
  this.name = name;
  this.marker = marker;
  this.sayName = function() {
    console.log(this.name)
  };
}

function Book(title, author, pages, hasRead) {
  this.title = title;
  this.author = author;
  this.pages = pages;
  this.hasRead = hasRead;
  this.info = function() {
      console.log(this.title)
      console.log(this.author)
      console.log(this.pages)
      console.log(this.hasRead)
  }
}

const player1 = new Player('steve', 'X');
const player2 = new Player('also steve', 'O');
player1.sayName(); // logs 'steve'
player2.sayName(); // logs 'also steve'
```

#### Prototype:

***This is an old way of coding, probably seen in legacy code***

If you create an object, it will inherit from the prototype object

- so it can use all the properties and methods from prototype

1. All objects in JavaScript have a prototype
2. Stated simply, the prototype is another object…
3. …that the original object inherits from, and has access to all of its prototype’s methods and properties



To actually see the prototype of an object, do this

```javascript
// player1 and player2 are objects already
Object.getPrototypeOf(player1) === Player.prototype; // returns true
Object.getPrototypeOf(player2) === Player.prototype; // returns true
```



You can also define a function in the object's prototype and every instance of the object can use it:

```javascript
Player.prototype.sayHello = function() {
   console.log("Hello, I'm a player!");
};

player1.sayHello(); // logs "Hello, I'm a player!"
player2.sayHello(); // logs "Hello, I'm a player!"

//this means
Object.getPrototypeOf(Player.prototype) === Object.prototype; // true
```

- This can save memory, if we define something in a centralized place it can help



Some useful methods:

Keys()

- returns an array of a given object's own enumerable string-keyed property names.

- ```javascript
  const object1 = {
    a: 'somestring',
    b: 42,
    c: false,
  };
  
  console.log(Object.keys(object1));
  // Expected output: Array ["a", "b", "c"]
  
  ```

  



### Symbol

```javascript
// TYPE 8 - Symbol - used to create unique identifiers for objects - more later..


```



### Function

```javascript
// TYPE 9 - well not really a type - Function

typeof alert // returns function

// while 'alert' is a function - there is no javascript data type called function - as functions are data type 'object' - the behavior of typeof is again wrong here
```

**functions** are data type **object**



## Map and filter



