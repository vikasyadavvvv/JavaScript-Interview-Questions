# JavaScript Interview Questions

## 1. What are the different data types in JavaScript?

### Answer:
JavaScript has two main categories of data types:

### Primitive Data Types (Immutable, stored by value):
- `String` - represents textual data
- `Number` - represents numeric values
- `BigInt` - represents arbitrary-length integers
- `Boolean` - represents logical values `true` or `false`
- `Undefined` - represents a variable that has been declared but not assigned a value
- `Null` - represents an intentional absence of any object value
- `Symbol` - represents unique and immutable identifiers

### Non-Primitive (Reference) Data Types:
- `Object` - represents collections of key-value pairs (includes:
  - `Array` - ordered lists
  - `Function` - callable objects
  - `Date` - date and time information
  - and other object types)

## Primitive Data Types
Basic, simple types of data.
They store only one value at a time.
They are immutable (cannot be changed directly).

## Non-Primitive (Reference) Data Types
More complex types.
They can store multiple values or a collection.
They are mutable (can be changed).


## 2. Difference between var, let and const

### Answer:

| Feature        | var                  | let                  | const                |
|---------------|----------------------|----------------------|----------------------|
| **Scope**     |  function            | Block                | Block                |
| **Hoisting**  | Hoisted and initialized with `undefined` | Hoisted but not initialized (Temporal Dead Zone) | Hoisted but not initialized (Temporal Dead Zone) |
| **Reassignment** | Can be updated      | Can be updated       | Cannot be updated    |
| **Redeclaration** | Can be redeclared | Cannot be redeclared in same scope | Cannot be redeclared |

### Code Examples:

```javascript
// var example
var x = 10;
var x = 20; // Allowed (redeclaration)
x = 30;     // Allowed (reassignment)
console.log(x); // 30

// let example
let y = 10;
// let y = 20; // Error: Cannot redeclare
y = 30;      // Allowed (reassignment)
console.log(y); // 30

// const example
const z = 10;
// const z = 20; // Error: Cannot redeclare
// z = 30;      // Error: Cannot reassign
console.log(z); // 10

// Scope example
function example() {
  var a = 1;
  let b = 2;
  const c = 3;
  
  if (true) {
    var a = 4; // Same variable
    let b = 5; // Different variable
    const c = 6; // Different variable
    console.log(a, b, c); // 4, 5, 6
  }
  
  console.log(a, b, c); // 4, 2, 3 (var leaked, let/const didn't)
}
example();
```


## 3. Hoisting in JavaScript

### Answer:
Hoisting in JavaScript is a behavior where variable and function declarations are moved to the top of their containing scope during the compilation phase, before code execution.

### Key Points:
- Only declarations are hoisted, not initializations
- `var` declarations are hoisted and initialized with `undefined`
- `let` and `const` declarations are hoisted but not initialized (Temporal Dead Zone)
- Function declarations are fully hoisted (can be called before declaration)
- Function expressions follow variable hoisting rules

### Code Examples:

```javascript
// Variable Hoisting Examples
console.log(a); // undefined (var is hoisted)
var a = 5;

// console.log(b); // ReferenceError (let is hoisted but not initialized)
let b = 10;

// console.log(c); // ReferenceError (const is hoisted but not initialized)
const c = 15;

// Function Hoisting Examples
foo(); // "Hello" (function declaration is fully hoisted)
function foo() {
  console.log("Hello");
}

// bar(); // TypeError (function expression follows variable hoisting rules)
var bar = function() {
  console.log("World");
};

// baz(); // ReferenceError (let/const function expressions aren't initialized)
let baz = function() {
  console.log("!");
};
```


## 4. Closures in JavaScript

### Answer:
In JavaScript, a closure is created when an inner function has access to variables from its outer (enclosing) function, even after the outer function has finished executing. The inner function "closes over" these variables, preserving them in memory.

### Key Characteristics:
- Closures have access to their own scope, outer function's variables, and global variables
- The outer function's variables remain in memory after execution
- Each closure maintains its own reference to these variables

### Code Examples:

```javascript
function Outter(){
    let a=10;
    let b=20;
    
    console.log(`Addition`,a+b)
    
    function Inner(){
        console.log(`Multiply`,a*b)
    }
    Inner()
}
Outter()
```


## 5. JavaScript Scopes (Variable Accessibility)

### Answer:
Scope determines where variables are accessible in your code. JavaScript has three main types of scope:

### 1. Global Scope
- Variables declared outside any function or block
- Accessible from anywhere in the code
- Can lead to naming collisions and pollution

### 2. Function Scope
- Variables declared inside a function
- Only accessible within that function
- Applies to `var` declarations

### 3. Block Scope
- Variables declared within curly braces `{}` (if statements, loops, etc.)
- Only accessible within that block
- Applies to `let` and `const` declarations

### Code Examples:

```javascript
// Global Scope
const globalVar = 'I am global';

function scopeDemo() {
  // Function Scope
  var functionVar = 'I am function scoped';
  let blockVar = 'I am block scoped';
  
  console.log(globalVar); // Accessible
  console.log(functionVar); // Accessible
  
  if (true) {
    // Block Scope
    let innerBlockVar = 'I am inner block';
    console.log(blockVar); // Accessible
  }
  
  // console.log(innerBlockVar); // ReferenceError - not accessible
}

scopeDemo();
// console.log(functionVar); // ReferenceError - not accessible

// Block Scope Example
{
  const blockScoped = 'Only available in this block';
  let anotherBlockVar = 'Same here';
}
// console.log(blockScoped); // ReferenceError
// console.log(anotherBlockVar); // ReferenceError

// var vs let/const in loops
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // Logs 3, 3, 3
}

for (let j = 0; j < 3; j++) {
  setTimeout(() => console.log(j), 100); // Logs 0, 1, 2
}
```


## 6. Difference between == and === in JavaScript

### Answer:
JavaScript has two equality comparison operators with different behaviors:

| Operator | Name           | Comparison Method               | Type Coercion |
|----------|----------------|----------------------------------|---------------|
| `==`     | Loose Equality | Checks value only               | Yes           |
| `===`    | Strict Equality| Checks both value and data type | No            |

### Key Differences:
- `==` performs type coercion before comparison
- `===` does not perform type coercion (safer)
- Always prefer `===` unless you specifically need type coercion

### Code Examples:

```javascript
// Loose equality (==) examples
console.log(5 == '5');      // true (type coercion)
console.log(true == 1);     // true
console.log(null == undefined); // true
console.log('' == 0);       // true
console.log([] == false);   // true
console.log([1,2] == '1,2'); // true

// Strict equality (===) examples
console.log(5 === '5');     // false (different types)
console.log(true === 1);    // false
console.log(null === undefined); // false
console.log('' === 0);      // false
console.log([] === false);  // false
console.log([1,2] === '1,2'); // false

// Special cases
console.log(NaN == NaN);   // false
console.log(NaN === NaN);  // false (use isNaN() instead)
console.log(0 == -0);      // true
console.log(0 === -0);     // true

// Object comparison
const obj1 = {a: 1};
const obj2 = {a: 1};

console.log(obj1 == obj2);  // false
console.log(obj1 === obj2); // false (different references)
console.log(obj1 == obj1);  // true
console.log(obj1 === obj1); // true (same reference)
```


## 7. Template Literals in JavaScript

### Answer:
Template literals are an ES6 feature that provide a modern way to work with strings in JavaScript. They use backticks (`` ` ``) instead of single or double quotes and offer powerful features like:
- Multi-line strings without escape characters
- String interpolation with embedded expressions
- Tagged templates for custom string processing

### Key Features:

```javascript
// Basic template literal
const name = 'Alice';
const greeting = `Hello, ${name}!`;
console.log(greeting); // "Hello, Alice!"

// Multi-line strings
const message = `
  This is a
  multi-line
  string
`;
console.log(message);

// Expression interpolation
const a = 5;
const b = 10;
console.log(`The sum is ${a + b}`); // "The sum is 15"

// Function calls in templates
function capitalize(str) {
  return str.toUpperCase();
}
console.log(`Shout: ${capitalize('hello')}`); // "Shout: HELLO"

// Tagged templates
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) => 
    `${result}${str}<span class="hl">${values[i] || ''}</span>`, '');
}

const user = 'Bob';
const age = 25;
const html = highlight`User ${user} is ${age} years old`;
// "<span class="hl">Bob</span> is <span class="hl">25</span> years old"
```


## 8. Callbacks in JavaScript

### Answer:
Callbacks are functions that are passed as arguments to other functions and are executed after a specific task completes. They are fundamental to asynchronous operations in JavaScript.

### Key Characteristics:
- **Asynchronous Control**: Handle operations that complete at unknown times
- **Higher-Order Functions**: Functions that accept other functions as arguments
- **Continuation Passing**: Pattern where control flows through callbacks

### Code Examples:

```javascript
// Basic callback example
function greet(name, callback) {
  console.log(`Hello, ${name}!`);
  callback();
}

function sayGoodbye() {
  console.log('Goodbye!');
}

greet('Alice', sayGoodbye);
// Output:
// Hello, Alice!
// Goodbye!

// Asynchronous callback (simulated with setTimeout)
function fetchData(callback) {
  setTimeout(() => {
    const data = { id: 1, name: 'John Doe' };
    callback(data);
  }, 1000);
}

fetchData((data) => {
  console.log('Data received:', data);
});

// Error-first callback pattern (Node.js convention)
function divide(a, b, callback) {
  if (b === 0) {
    callback(new Error('Cannot divide by zero'), null);
  } else {
    callback(null, a / b);
  }
}

divide(10, 2, (err, result) => {
  if (err) {
    console.error('Error:', err.message);
  } else {
    console.log('Result:', result);
  }
});

// Callback in array method
const numbers = [1, 2, 3, 4];
const doubled = numbers.map((num) => num * 2);
console.log(doubled); // [2, 4, 6, 8]
```


## 9. Null vs Undefined in JavaScript

### Answer:
JavaScript has two distinct primitive values representing absence of value:

| Value      | Type      | Meaning                                                                 |
|------------|-----------|-------------------------------------------------------------------------|
| `null`     | object    | Intentional absence of any object value (explicit "nothing")            |
| `undefined`| undefined | Variable declared but not assigned, or missing object property         |

### Key Differences:

```javascript
// Undefined examples
let unassignedVar;
console.log(unassignedVar); // undefined

const obj = {};
console.log(obj.nonExistentProp); // undefined

function missingParam(param) {
  console.log(param); // undefined when called without argument
}
missingParam();

// Null examples
const explicitNull = null;
console.log(explicitNull); // null

const user = { name: 'Alice', address: null }; // Explicitly no address
console.log(user.address); // null

// Comparison
console.log(typeof null);      // 'object' (historical bug)
console.log(typeof undefined); // 'undefined'

console.log(null == undefined);   // true (loose equality)
console.log(null === undefined);  // false (strict equality)

// Practical usage
function getValue(mightBeNull) {
  return mightBeNull ?? 'default value'; // Nullish coalescing
}

console.log(getValue(null));      // 'default value'
console.log(getValue(undefined)); // 'default value'
console.log(getValue(0));         // 0
```


## 10. Function Declarations vs Expressions in JavaScript

### A function declaration is when you create a function using the `function` keyword followed by a name. This is the most basic way to define a function in JavaScript.

```javascript
// Function Declaration Syntax
function functionName(parameters) {
  // function body
  return value;
}
```
### A function expression occurs when you assign a function to a variable. Unlike declarations, these are not hoisted and must be defined before use.

```javascript
// Basic Function Expression
const greet = function(name) {
  return `Hello, ${name}!`;
};
```


## 11. Understanding `this` in JavaScript

## What is `this`?
In JavaScript, `this` refers to the execution context - the object that "owns" the currently executing code. Its value changes depending on how a function is called.

## Basic Rules of `this`

In the global scope, `this` refers to the global object (`window` in browsers, `global` in Node.js).

```javascript
console.log(this); // Window {...} (in browser)
```

```
const person = {
  name: 'John',
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
};
person.greet(); // "Hello, my name is John"
```


## 12. Arrow Functions vs Regular Functions in JavaScript

## Key Difference: `this` Binding

Arrow functions are shorter and cleaner, and they inherit `this` from their parent scope. This makes them ideal for:
- Callbacks
- Methods where you want to preserve the outer context

```javascript
// Regular function - has its own `this`
const obj1 = {
  count: 0,
  increment: function() {
    setInterval(function() {
      this.count++; // ❌ Wrong `this` (points to window)
      console.log(this.count); // NaN
    }, 1000);
  }
};

// Arrow function - inherits `this` from parent
const obj2 = {
  count: 0,
  increment: function() {
    setInterval(() => {
      this.count++; // ✅ Correct `this` (points to obj2)
      console.log(this.count); // 1, 2, 3...
    }, 1000);
  }
};
```


## 13.# IIFE (Immediately Invoked Function Expression) in JavaScript

## What is an IIFE?
An IIFE is a JavaScript function that runs as soon as it is defined. The syntax consists of two main parts:
1. The function expression wrapped in parentheses `(function(){...})`
2. The immediate execution parentheses `()`
3. Why Use IIFEs?
 Avoid Polluting Global Scope
IIFEs create a private scope where variables don't leak to the global scope.

```javascript
// Basic IIFE Syntax
(function() {
  console.log('This runs immediately!');
})();
```


## 13. JavaScript Destructuring

Destructuring allows you to unpack values from arrays or properties from objects into distinct variables.

## Object Destructuring

### Basic Syntax
```javascript
const person = { name: 'John', age: 30 };

// Traditional way
const name = person.name;
const age = person.age;

// With destructuring
const { name, age } = person;
```


## 14. Shallow clone and Deep Clone in javascript (How to Clone Object)

### A shallow clone creates a new object/array, but it only copies the first level of properties.
If the object has nested objects (or arrays), the clone will still reference the same nested objects in memory.

👉 Meaning: If you change something in the nested object of the clone, it will also affect the original.
```javascript
let obj1 = {
  name: "Vikas",
  address: {
    city: "Mumbai",
    pincode: 400070
  }
};

// Shallow clone using spread
let obj2 = { ...obj1 };

obj2.name = "Rahul"; // changes only obj2
obj2.address.city = "Delhi"; // changes both obj1 and obj2 because 'address' is shared

console.log(obj1.address.city); // "Delhi"

```
### A deep Clone creates a completely independent copy of the object, including all nested objects/arrays.
So, changing the clone will not affect the original at any level.
```javascript
let obj1 = {
  name: "Vikas",
  address: {
    city: "Mumbai",
    pincode: 400070
  }
};

// Deep clone using JSON methods
let obj2 = JSON.parse(JSON.stringify(obj1));

obj2.name = "Rahul";
obj2.address.city = "Delhi";

console.log(obj1.address.city); // "Mumbai" (original is safe)

```
⚡ Ways to Clone
Shallow Clone:
- Spread operator: { ...obj }
- Object.assign({}, obj)
- Array.slice() or [...array]

Deep Clone:
- JSON.parse(JSON.stringify(obj) (simple but fails for functions, Date, Map, Set, etc.)
- structuredClone(obj) (modern, supports most types except functions)



## 15. What are Getters and Setters?

In JavaScript, getters and setters are special methods that let you control how properties of an object are accessed (read) and modified (written).

- Getter (get) → Used to access a property (like a function but looks like a property).
- Setter (set) → Used to change a property (can add validation, transform data, etc.).

```javascript
let person = {
  firstName: "Vikas",
  lastName: "Yadav",

  // Getter
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },

  // Setter
  set fullName(name) {
    let parts = name.split(" ");
    this.firstName = parts[0];
    this.lastName = parts[1];
  }
};

// Using getter
console.log(person.fullName); // "Vikas Yadav" (no parentheses needed)

// Using setter
person.fullName = "Rahul Sharma";
console.log(person.firstName); // "Rahul"
console.log(person.lastName);  // "Verma"
```


## 16. What is the Event Loop?

JavaScript is single-threaded (it executes one thing at a time).
But it can handle asynchronous tasks (like API calls, setTimeout, promises) without blocking the main thread.
👉 The Event Loop is the mechanism that makes this possible.

## 17. What is Promise ?
A Promise is an object in JavaScript that represents an asynchronous task.
- It executes some work (like API calls, file reading, timers, etc.) and will either:
- succeed (fulfilled) → return a value
- fail (rejected) → return an error

 It has 3 states:
- Pending – initial state, still running
- Fulfilled – task finished successfully
- Rejected – task failed

 To handle results:
- .then() → runs when the promise is fulfilled (success)
- .catch() → runs when the promise is rejected (error)
- .finally() → runs no matter what (cleanup work)

👉 In short: Promises are used to handle asynchronous operations (like API calls) in a cleaner and more manageable way than callbacks.
```javascript
let promise = new Promise((resolve, reject) => {
  let dataFetched = true;

  if (dataFetched) {
    resolve("✅ Data fetched successfully");
  } else {
    reject("❌ Failed to fetch data");
  }
});

// Handling the promise
promise
  .then(result => console.log(result))   // if resolved
  .catch(error => console.log(error))    // if rejected
  .finally(() => console.log("Done"));   // always runs

```

## 17. What is async/await in JavaScript?

async and await are keywords in JavaScript that make working with asynchronous code easier and more readable, compared to using callbacks or .then() with promises.
async function
Declares a function as asynchronous.
Always returns a Promise, even if you return a simple value.
await keyword
Can only be used inside an async function.
Waits for a Promise to resolve and returns the resolved value.
Makes asynchronous code look synchronous.
```javascript
// A function that returns a Promise
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data received!");
    }, 2000); // simulating 2-second delay
  });
}

// Using async/await
async function getData() {
  console.log("Fetching data...");
  
  const result = await fetchData(); // wait for fetchData() to resolve
  console.log(result); // "Data received!"
  
  console.log("Process completed.");
}

getData();

```

