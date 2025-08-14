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

## 2. Difference between var, let and const

### Answer:

| Feature        | var                  | let                  | const                |
|---------------|----------------------|----------------------|----------------------|
| **Scope**     | Global or function   | Block                | Block                |
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
