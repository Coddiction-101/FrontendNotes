# ⚡ JavaScript & React — Complete Mastery Notes
### For Interviews · Internships · Placements · Projects

> **How to use these notes:** Read top to bottom for learning. Use the Table of Contents to jump to specific topics for quick revision. Every concept has simple explanations + real code examples.

---

## 📚 Table of Contents

### Part 1 — JavaScript
1. [JS Fundamentals](#1-js-fundamentals)
2. [Variables — var, let, const](#2-variables--var-let-const)
3. [Data Types & Type Coercion](#3-data-types--type-coercion)
4. [Operators & Expressions](#4-operators--expressions)
5. [Control Flow](#5-control-flow)
6. [Functions — All Variants](#6-functions--all-variants)
7. [Scope, Closures & Hoisting](#7-scope-closures--hoisting)
8. [Arrays — Deep Dive](#8-arrays--deep-dive)
9. [Objects — Deep Dive](#9-objects--deep-dive)
10. [Destructuring & Spread/Rest](#10-destructuring--spreadrest)
11. [Classes & Prototypes](#11-classes--prototypes)
12. [Asynchronous JavaScript](#12-asynchronous-javascript)
13. [ES6+ Modern Features](#13-es6-modern-features)
14. [DOM Manipulation](#14-dom-manipulation)
15. [Events & Event Loop](#15-events--event-loop)
16. [Error Handling](#16-error-handling)
17. [Modules (ESM)](#17-modules-esm)
18. [JS Design Patterns](#18-js-design-patterns)

### Part 2 — React
19. [React Core Concepts](#19-react-core-concepts)
20. [JSX](#20-jsx)
21. [Components — Functional & Class](#21-components--functional--class)
22. [Props](#22-props)
23. [State & useState](#23-state--usestate)
24. [useEffect Hook](#24-useeffect-hook)
25. [All React Hooks](#25-all-react-hooks)
26. [Context API](#26-context-api)
27. [React Router](#27-react-router)
28. [State Management (Redux / Zustand)](#28-state-management-redux--zustand)
29. [Performance Optimization](#29-performance-optimization)
30. [Forms in React](#30-forms-in-react)
31. [Custom Hooks](#31-custom-hooks)
32. [React Patterns](#32-react-patterns)
33. [Testing in React](#33-testing-in-react)
34. [Interview Q&A — JS](#34-interview-qa--js)
35. [Interview Q&A — React](#35-interview-qa--react)
36. [Coding Problems Cheatsheet](#36-coding-problems-cheatsheet)

---

# PART 1 — JAVASCRIPT

---

## 1. JS Fundamentals

### What is JavaScript?

JavaScript is a **high-level, interpreted, single-threaded, dynamically-typed** programming language. It was originally created for the browser but now runs everywhere via **Node.js**.

```
Browser Request
      ↓
   HTML/CSS   →  Structure + Style
      +
  JavaScript  →  Behaviour + Interactivity
```

### How JS Runs in the Browser

1. Browser downloads HTML
2. Finds a `<script>` tag
3. **JS Engine** (V8 in Chrome, SpiderMonkey in Firefox) parses and executes JS
4. Result: dynamic UI, data fetching, animations, etc.

### Adding JS to HTML

```html
<!-- Inline (avoid for large code) -->
<script>
  console.log("Hello!");
</script>

<!-- External file (recommended) -->
<script src="app.js"></script>

<!-- Defer — download in parallel, execute AFTER HTML parsed -->
<script defer src="app.js"></script>

<!-- Async — download in parallel, execute AS SOON AS downloaded -->
<script async src="analytics.js"></script>
```

> 💡 **Rule:** Always use `defer` for your main script. Use `async` only for independent scripts (analytics, ads).

### Console Methods

```javascript
console.log("Regular output");
console.warn("⚠️ Warning");
console.error("❌ Error");
console.table([{ name: "Alice", age: 25 }]); // Tabular display
console.group("Group Name");
  console.log("inside group");
console.groupEnd();
console.time("timer");
  // some code
console.timeEnd("timer"); // Shows elapsed time
console.assert(1 === 2, "This will print!"); // Print if condition is false
console.clear(); // Clear console
```

---

## 2. Variables — var, let, const

This is one of the **most asked** topics in interviews!

### `var` — The Old Way (Avoid!)

```javascript
var name = "Alice";
var name = "Bob"; // ✅ Re-declaration allowed (bad!)
name = "Charlie"; // ✅ Re-assignment allowed

// var is FUNCTION-scoped (not block-scoped)
function test() {
  if (true) {
    var x = 10;
  }
  console.log(x); // 10 — x leaks out of the if block!
}

// var is HOISTED to the top of its function
console.log(y); // undefined (not an error!)
var y = 5;
// Internally treated as:
// var y;        ← hoisted
// console.log(y); → undefined
// y = 5;
```

### `let` — Block-Scoped (Use for variables that change)

```javascript
let count = 0;
// let count = 1; // ❌ Re-declaration NOT allowed
count = 1;        // ✅ Re-assignment allowed

// let is BLOCK-scoped
if (true) {
  let blockVar = "I'm in a block";
  console.log(blockVar); // Works
}
// console.log(blockVar); // ❌ ReferenceError — not accessible outside block

// let is hoisted but NOT initialized (Temporal Dead Zone)
// console.log(z); // ❌ ReferenceError: Cannot access before initialization
let z = 5;
```

### `const` — Block-Scoped (Use for variables that don't change)

```javascript
const PI = 3.14159;
// PI = 3; // ❌ Assignment to constant variable

// IMPORTANT: const objects/arrays are NOT frozen!
const person = { name: "Alice", age: 25 };
person.age = 26;      // ✅ Modifying property is allowed
person.city = "NYC";  // ✅ Adding property is allowed
// person = {};       // ❌ Re-assigning the variable is NOT allowed

const arr = [1, 2, 3];
arr.push(4);          // ✅ Modifying array is allowed
// arr = [5, 6];      // ❌ Re-assigning is NOT allowed

// To truly freeze an object:
const frozen = Object.freeze({ name: "Bob" });
frozen.name = "Alice"; // Silently fails (or throws in strict mode)
```

### Comparison Table

| Feature | `var` | `let` | `const` |
|---------|-------|-------|---------|
| Scope | Function | Block | Block |
| Re-declare | ✅ | ❌ | ❌ |
| Re-assign | ✅ | ✅ | ❌ |
| Hoisted | ✅ (undefined) | ✅ (TDZ) | ✅ (TDZ) |
| Global object property | ✅ | ❌ | ❌ |

> 📝 **Interview Tip:** Use `const` by default. Use `let` only when you need to reassign. Never use `var`.

---

## 3. Data Types & Type Coercion

### Primitive Types (7 types)

```javascript
// 1. Number
let age = 25;
let price = 9.99;
let notANumber = NaN;       // Result of invalid math: "abc" * 2
let infinity = Infinity;    // 1/0

// 2. String
let name = "Alice";
let greeting = `Hello, ${name}!`; // Template literal

// 3. Boolean
let isActive = true;
let isLoggedIn = false;

// 4. undefined — variable declared but not assigned
let x;
console.log(x); // undefined

// 5. null — intentional absence of value
let user = null; // "There is no user"

// 6. Symbol — unique identifier (ES6+)
const id1 = Symbol("id");
const id2 = Symbol("id");
console.log(id1 === id2); // false — always unique!

// 7. BigInt — for very large integers (ES2020)
const bigNum = 9007199254740991n; // Add 'n' suffix
const alsoLarge = BigInt("9007199254740991");
```

### Reference Types

```javascript
// Objects, Arrays, Functions are all objects in JS
typeof {}         // "object"
typeof []         // "object" (not "array"!)
typeof function(){} // "function"
typeof null       // "object" ← famous JS bug!

// Check for array properly:
Array.isArray([]) // true
```

### `typeof` Operator

```javascript
typeof 42           // "number"
typeof "hello"      // "string"
typeof true         // "boolean"
typeof undefined    // "undefined"
typeof null         // "object"   ← bug!
typeof Symbol()     // "symbol"
typeof 42n          // "bigint"
typeof {}           // "object"
typeof []           // "object"
typeof function(){} // "function"
```

### Type Coercion — The Tricky Part

```javascript
// IMPLICIT coercion (JS does it automatically)

// String + Number → String (concatenation wins)
"5" + 3       // "53"  — number becomes string
"5" - 3       // 2     — string becomes number
"5" * "2"     // 10    — both become numbers
"5" - "abc"   // NaN   — "abc" can't be a number

// Comparison coercion
0 == false    // true  — both coerce to 0
1 == true     // true  — both coerce to 1
"" == false   // true  — both coerce to 0
null == undefined // true — special case
null == 0     // false — null only equals undefined

// Strict equality — NO coercion
0 === false   // false — different types
"1" === 1     // false — different types

// Falsy values (coerce to false in boolean context)
// false, 0, -0, 0n, "", '', ``, null, undefined, NaN
Boolean(0)         // false
Boolean("")        // false
Boolean(null)      // false
Boolean(undefined) // false
Boolean(NaN)       // false

// Truthy values — everything else
Boolean(1)         // true
Boolean("0")       // true — non-empty string!
Boolean([])        // true — empty array!
Boolean({})        // true — empty object!

// EXPLICIT coercion
Number("42")       // 42
Number("")         // 0
Number(null)       // 0
Number(undefined)  // NaN
Number(true)       // 1
Number(false)      // 0

String(42)         // "42"
String(null)       // "null"
String(undefined)  // "undefined"

Boolean(0)         // false
Boolean("hello")   // true

parseInt("42px")   // 42  — reads until non-numeric
parseFloat("3.14") // 3.14
parseInt("0xFF", 16) // 255 — second arg is radix (base)
```

> 🚨 **Famous JS Interview Quirks:**
> ```javascript
> [] + []   // ""     (both convert to "" and concatenate)
> [] + {}   // "[object Object]"
> {} + []   // 0      (JS sees {} as empty block, + as unary plus on [])
> +"3"      // 3      (unary plus converts to number)
> !!"hello" // true   (double negation converts to boolean)
> ```

---

## 4. Operators & Expressions

### Nullish Coalescing `??` vs OR `||`

```javascript
// || returns right side if LEFT is FALSY
0 || "default"        // "default" — 0 is falsy!
"" || "default"       // "default" — "" is falsy!
false || "default"    // "default"

// ?? returns right side only if LEFT is null or undefined
0 ?? "default"        // 0     — 0 is NOT null/undefined
"" ?? "default"       // ""    — "" is NOT null/undefined
null ?? "default"     // "default"
undefined ?? "default" // "default"

// Real-world difference:
const port = userConfig.port || 3000; // Bug! If port=0, uses 3000
const port2 = userConfig.port ?? 3000; // Correct! 0 is valid port
```

### Optional Chaining `?.`

```javascript
// Without optional chaining
const city = user && user.address && user.address.city; // verbose

// With optional chaining — returns undefined instead of throwing error
const city = user?.address?.city;

// With methods
user?.getProfile?.(); // Call only if getProfile exists

// With arrays
const first = arr?.[0];

// Real-world use
const name = response?.data?.user?.name ?? "Anonymous";
```

### Spread `...` and Rest `...`

```javascript
// SPREAD — expands iterables
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2]; // [1,2,3,4,5,6]
const copy = [...arr1]; // Shallow copy

// Spread with objects
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, ...obj1 }; // { c:3, a:1, b:2 }
const updated = { ...obj1, b: 99 }; // { a:1, b:99 } — override b

// Spread in function calls
Math.max(...arr1); // Same as Math.max(1, 2, 3)

// REST — collects remaining items into array
function sum(...numbers) {      // all args collected into array
  return numbers.reduce((a, b) => a + b, 0);
}
sum(1, 2, 3, 4); // 10

function first(a, b, ...rest) {
  console.log(a);    // 1
  console.log(b);    // 2
  console.log(rest); // [3, 4, 5]
}
first(1, 2, 3, 4, 5);
```

---

## 5. Control Flow

### if / else if / else

```javascript
const score = 85;

if (score >= 90) {
  console.log("A");
} else if (score >= 80) {
  console.log("B"); // This runs
} else if (score >= 70) {
  console.log("C");
} else {
  console.log("F");
}

// Ternary operator
const grade = score >= 60 ? "Pass" : "Fail";

// Short-circuit evaluation
const name = user?.name || "Guest"; // If no name, use "Guest"
isLoggedIn && showDashboard();       // Run only if logged in
```

### switch

```javascript
const day = "Monday";

switch (day) {
  case "Saturday":
  case "Sunday":           // Fall-through — both match same block
    console.log("Weekend");
    break;
  case "Monday":
  case "Tuesday":
  case "Wednesday":
  case "Thursday":
  case "Friday":
    console.log("Weekday"); // This runs
    break;
  default:
    console.log("Unknown day");
}

// switch uses === (strict equality)
```

### Loops

```javascript
// for loop
for (let i = 0; i < 5; i++) {
  console.log(i); // 0 1 2 3 4
}

// while
let count = 0;
while (count < 3) {
  console.log(count++); // 0 1 2
}

// do...while (runs at least once)
do {
  console.log("runs once even if false");
} while (false);

// for...of — iterate VALUES of iterables (arrays, strings, Maps, Sets)
const fruits = ["apple", "banana", "mango"];
for (const fruit of fruits) {
  console.log(fruit);
}

for (const char of "hello") {
  console.log(char); // h e l l o
}

// for...in — iterate KEYS of objects (use carefully!)
const person = { name: "Alice", age: 25 };
for (const key in person) {
  console.log(`${key}: ${person[key]}`);
}
// Warning: for...in also iterates over inherited properties
// Safer: Object.keys(person).forEach(key => ...)

// Loop control
for (let i = 0; i < 10; i++) {
  if (i === 3) continue; // Skip 3
  if (i === 7) break;    // Stop at 7
  console.log(i);        // 0 1 2 4 5 6
}

// Labeled break (for nested loops)
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (j === 1) break outer; // Break both loops
  }
}
```

---

## 6. Functions — All Variants

### Function Declaration

```javascript
// Can be called BEFORE it's defined (hoisted)
sayHello(); // Works!

function sayHello() {
  console.log("Hello!");
}

// Parameters with defaults
function greet(name = "World", greeting = "Hello") {
  return `${greeting}, ${name}!`;
}
greet();            // "Hello, World!"
greet("Alice");     // "Hello, Alice!"
greet("Bob", "Hi"); // "Hi, Bob!"
```

### Function Expression

```javascript
// NOT hoisted — must be defined before calling
// const sayHi = () => {}; // would throw error if called first

const sayHi = function(name) {
  return `Hi, ${name}!`;
};

// Named function expression (name only available inside)
const factorial = function fact(n) {
  return n <= 1 ? 1 : n * fact(n - 1); // Can use 'fact' inside
};
```

### Arrow Functions

```javascript
// Arrow functions — concise syntax, no own `this`

// Traditional
function add(a, b) { return a + b; }

// Arrow — single expression (implicit return)
const add = (a, b) => a + b;

// Arrow — with body
const greet = (name) => {
  const msg = `Hello, ${name}!`;
  return msg; // Explicit return needed with {}
};

// Single parameter — parens optional
const double = n => n * 2;

// No parameters
const greetAll = () => "Hello everyone!";

// Returning an object — wrap in parens!
const makeUser = (name, age) => ({ name, age }); // ✅
// const makeUser = (name, age) => { name, age }; // ❌ {} is body, not object!

// KEY DIFFERENCE: Arrow functions have NO own `this`
const timer = {
  seconds: 0,
  start() {
    // 'this' here is the timer object
    setInterval(() => {
      this.seconds++; // Arrow function inherits 'this' from start()
      console.log(this.seconds);
    }, 1000);
  }
};

// If we used regular function inside setInterval:
// this.seconds++ would fail because 'this' would be window/undefined
```

### Immediately Invoked Function Expressions (IIFE)

```javascript
// Runs immediately, creates its own scope
(function() {
  const private_var = "Can't access me outside!";
  console.log("IIFE ran!");
})();

// Arrow IIFE
(() => {
  console.log("Arrow IIFE!");
})();

// Use case: avoid polluting global scope
(function() {
  var localConfig = { ... }; // Stays local
})();
```

### Higher-Order Functions

```javascript
// A function that takes or returns another function

// Takes a function as argument
function applyTwice(fn, value) {
  return fn(fn(value));
}
const double = x => x * 2;
applyTwice(double, 3); // 12 (3 → 6 → 12)

// Returns a function (closure)
function multiplier(factor) {
  return (number) => number * factor; // Returns a new function
}
const triple = multiplier(3);
triple(5); // 15
triple(7); // 21

// Real examples: .map(), .filter(), .reduce() are all HOFs
```

---

## 7. Scope, Closures & Hoisting

### Scope — Where Variables are Accessible

```javascript
// Global scope
let globalVar = "I'm global";

function outer() {
  // Function scope
  let outerVar = "I'm in outer";

  function inner() {
    // Nested function scope
    let innerVar = "I'm in inner";

    // Can access all outer scopes (Scope Chain)
    console.log(innerVar);  // ✅
    console.log(outerVar);  // ✅
    console.log(globalVar); // ✅
  }

  // console.log(innerVar); // ❌ ReferenceError
}

// Block scope (let and const)
{
  let blockVar = "block";
  const blockConst = "also block";
  var notBlocked = "leaks!"; // var ignores blocks
}
// console.log(blockVar);   // ❌ ReferenceError
// console.log(blockConst); // ❌ ReferenceError
console.log(notBlocked);    // ✅ "leaks!" (var leaks out!)
```

### Closures — One of the Most Important JS Concepts

```javascript
// A closure is when a function REMEMBERS variables from its outer scope
// even after the outer function has returned.

function makeCounter() {
  let count = 0; // This variable is "closed over"

  return {
    increment() { count++; },
    decrement() { count--; },
    getCount()  { return count; }
  };
}

const counter = makeCounter();
counter.increment();
counter.increment();
counter.increment();
counter.decrement();
console.log(counter.getCount()); // 2

// count is private! No direct access.
// console.log(counter.count); // undefined

// Real-world closure examples:

// 1. Data encapsulation / private variables
function createUser(name) {
  let _role = "user"; // private
  return {
    getName: () => name,
    getRole: () => _role,
    setRole: (role) => { _role = role; }
  };
}

// 2. Function factories
function createMultiplier(x) {
  return (y) => x * y; // x is closed over
}
const double = createMultiplier(2);
const triple = createMultiplier(3);
double(5); // 10
triple(5); // 15

// 3. Classic interview trap — var in loop
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000); // prints 3, 3, 3 — NOT 0, 1, 2!
}
// Why? var i is function-scoped, by the time timeout runs, loop is done and i=3

// Fix 1: Use let (block-scoped, each iteration has own i)
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000); // prints 0, 1, 2 ✅
}

// Fix 2: IIFE closure
for (var i = 0; i < 3; i++) {
  ((capturedI) => {
    setTimeout(() => console.log(capturedI), 1000);
  })(i);
}
```

### Hoisting

```javascript
// Hoisting = variable/function declarations are moved to the top
// of their scope during compilation phase (before code runs)

// --- Function declarations are FULLY hoisted ---
greet(); // ✅ Works! "Hello!"
function greet() { console.log("Hello!"); }

// --- var is HOISTED but NOT initialized (value stays undefined) ---
console.log(x); // undefined (not an error!)
var x = 5;
console.log(x); // 5

// Internally interpreted as:
// var x;           // ← hoisted declaration
// console.log(x);  // undefined
// x = 5;           // ← assignment stays in place
// console.log(x);  // 5

// --- let and const are hoisted but in TEMPORAL DEAD ZONE (TDZ) ---
// console.log(y);  // ❌ ReferenceError: Cannot access 'y' before initialization
let y = 10;

// --- Function expressions are NOT fully hoisted ---
// sayHi(); // ❌ ReferenceError
const sayHi = () => "Hi!";
```

---

## 8. Arrays — Deep Dive

### Creating & Accessing

```javascript
const arr = [1, 2, 3, 4, 5];

arr[0];          // 1 — first element
arr[arr.length - 1]; // 5 — last element
arr.at(-1);      // 5 — last element (ES2022)
arr.at(-2);      // 4 — second from last

// Checking
Array.isArray(arr);    // true
arr.length;            // 5
arr.includes(3);       // true
arr.indexOf(3);        // 2
arr.lastIndexOf(3);    // 2
```

### Mutating Methods (Modify original array)

```javascript
const arr = [1, 2, 3];

// Adding
arr.push(4, 5);       // Add to end → [1,2,3,4,5], returns new length
arr.unshift(0);       // Add to beginning → [0,1,2,3,4,5], returns new length

// Removing
arr.pop();            // Remove from end → returns removed element
arr.shift();          // Remove from beginning → returns removed element

// splice — most powerful: add, remove, replace at any position
arr.splice(1, 2);         // Remove 2 elements starting at index 1
arr.splice(1, 0, "a","b");// Insert at index 1 without removing
arr.splice(1, 1, "x");    // Replace 1 element at index 1 with "x"

// sort — MUTATES! Default sorts as STRINGS (careful with numbers!)
["banana","apple","cherry"].sort(); // ["apple","banana","cherry"]
[10, 1, 21, 2].sort();             // [1, 10, 2, 21] — WRONG for numbers!
[10, 1, 21, 2].sort((a, b) => a - b); // [1, 2, 10, 21] — correct

// reverse — MUTATES
[1, 2, 3].reverse(); // [3, 2, 1]

// fill — MUTATES
[1, 2, 3, 4, 5].fill(0, 2, 4); // [1, 2, 0, 0, 5]
```

### Non-Mutating Methods (Return new array/value)

```javascript
const nums = [1, 2, 3, 4, 5];

// map — transform each element → returns new array
nums.map(n => n * 2);           // [2, 4, 6, 8, 10]
nums.map((n, i) => `${i}:${n}`);// ["0:1", "1:2", ...]

// filter — keep elements that match condition → returns new array
nums.filter(n => n % 2 === 0);  // [2, 4]
nums.filter(n => n > 3);        // [4, 5]

// reduce — accumulate to single value
nums.reduce((acc, curr) => acc + curr, 0);   // 15 (sum)
nums.reduce((acc, curr) => acc * curr, 1);   // 120 (product)

// reduce to build an object
const people = [
  { name: "Alice", dept: "Engineering" },
  { name: "Bob",   dept: "Marketing" },
  { name: "Carol", dept: "Engineering" }
];
const byDept = people.reduce((acc, person) => {
  (acc[person.dept] = acc[person.dept] || []).push(person.name);
  return acc;
}, {});
// { Engineering: ["Alice", "Carol"], Marketing: ["Bob"] }

// find — returns FIRST element that matches (or undefined)
nums.find(n => n > 3);          // 4

// findIndex — returns INDEX of first match (or -1)
nums.findIndex(n => n > 3);     // 3

// some — true if AT LEAST ONE matches
nums.some(n => n > 4);          // true

// every — true if ALL match
nums.every(n => n > 0);         // true
nums.every(n => n > 3);         // false

// flat — flatten nested arrays
[1, [2, [3, [4]]]].flat();      // [1, 2, [3, [4]]] — 1 level
[1, [2, [3, [4]]]].flat(Infinity); // [1, 2, 3, 4] — all levels

// flatMap — map then flat (1 level)
[[1,2],[3,4]].flatMap(x => x);  // [1,2,3,4]
nums.flatMap(n => [n, n * 2]);  // [1,2, 2,4, 3,6, 4,8, 5,10]

// slice — extract portion WITHOUT modifying original
nums.slice(1, 3);               // [2, 3] (start inclusive, end exclusive)
nums.slice(-2);                 // [4, 5] (last 2)
nums.slice();                   // [1,2,3,4,5] — copy!

// concat — merge arrays
[1, 2].concat([3, 4], [5]);     // [1,2,3,4,5]

// join — array to string
["a","b","c"].join("-");        // "a-b-c"
["a","b","c"].join("");         // "abc"

// indexOf / lastIndexOf / includes
nums.indexOf(3);                // 2
nums.includes(3);               // true

// Array.from — create array from array-like or iterable
Array.from("hello");            // ["h","e","l","l","o"]
Array.from({length: 5}, (_, i) => i); // [0,1,2,3,4]
Array.from(new Set([1,2,2,3])); // [1,2,3] (deduplicate!)

// Array.of
Array.of(1, 2, 3);             // [1,2,3]

// Chaining
const result = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  .filter(n => n % 2 === 0)    // [2,4,6,8,10]
  .map(n => n ** 2)            // [4,16,36,64,100]
  .reduce((a, b) => a + b, 0); // 220
```

---

## 9. Objects — Deep Dive

### Creating Objects

```javascript
// Object literal (most common)
const person = {
  name: "Alice",
  age: 25,
  "full name": "Alice Smith", // Key with space needs quotes
  greet() {                   // Method shorthand (ES6+)
    return `Hi, I'm ${this.name}`;
  },
  // Old way: greet: function() { ... }
};

// Constructor function (old way)
function Person(name, age) {
  this.name = name;
  this.age = age;
}
const p1 = new Person("Bob", 30);

// Object.create() — set prototype explicitly
const animal = { breathe() { return "breathing"; } };
const dog = Object.create(animal);
dog.bark = () => "Woof!";
dog.breathe(); // "breathing" — inherited from animal

// Class syntax (modern, covered in Section 11)
```

### Accessing & Modifying

```javascript
const person = { name: "Alice", age: 25 };

// Dot notation (use when key is known and valid identifier)
person.name;             // "Alice"
person.age = 26;         // Modify

// Bracket notation (use for dynamic keys or keys with spaces)
person["name"];          // "Alice"
const key = "age";
person[key];             // 25 — dynamic access!
person["full name"];     // For keys with spaces

// Adding properties
person.email = "alice@example.com";

// Deleting properties
delete person.age;

// Checking if property exists
"name" in person;              // true (checks prototype chain too)
person.hasOwnProperty("name"); // true (only own properties)
Object.hasOwn(person, "name"); // true (ES2022, preferred)
```

### Object Methods

```javascript
const obj = { a: 1, b: 2, c: 3 };

// Get keys, values, entries
Object.keys(obj);    // ["a", "b", "c"]
Object.values(obj);  // [1, 2, 3]
Object.entries(obj); // [["a",1], ["b",2], ["c",3]]

// Loop using entries
for (const [key, value] of Object.entries(obj)) {
  console.log(`${key}: ${value}`);
}

// Create from entries
Object.fromEntries([["a",1],["b",2]]); // { a:1, b:2 }
Object.fromEntries(new Map([["a",1]])); // {a:1}

// Merging with Object.assign
const merged = Object.assign({}, obj, { d: 4 }); // { a:1, b:2, c:3, d:4 }
const merged2 = { ...obj, d: 4 };                 // Same result, cleaner

// Freezing and sealing
const frozen = Object.freeze({ x: 1 }); // Can't add, remove, or modify
frozen.x = 99;  // Silently ignored (strict mode throws)

const sealed = Object.seal({ x: 1 });  // Can modify but not add/remove
sealed.x = 99;  // ✅ Works
sealed.y = 2;   // ❌ Ignored

// Object.create for prototype chain
// Covered in Section 11 (Prototypes)
```

### `this` Keyword — Critical Concept

```javascript
// 'this' refers to the object that CALLS the function (not where it's defined)

// 1. In methods — this = the object
const person = {
  name: "Alice",
  greet() {
    return `Hi, I'm ${this.name}`; // this = person
  }
};
person.greet(); // "Hi, I'm Alice"

// 2. Function call — this = window (browser) or undefined (strict mode)
function show() {
  console.log(this); // window or undefined
}

// 3. Arrow functions — NO own this, inherit from enclosing scope
const obj = {
  name: "Bob",
  arrowMethod: () => {
    console.log(this.name); // undefined! Arrow inherits global this
  },
  regularMethod() {
    const inner = () => {
      console.log(this.name); // "Bob" — inherits from regularMethod's this
    };
    inner();
  }
};

// 4. Explicit binding — call, apply, bind
function greet(greeting, punctuation) {
  return `${greeting}, ${this.name}${punctuation}`;
}

const user = { name: "Charlie" };

greet.call(user, "Hello", "!");       // Calls immediately, args listed
greet.apply(user, ["Hello", "!"]);    // Calls immediately, args in array
const boundGreet = greet.bind(user);  // Returns NEW function, doesn't call
boundGreet("Hi", ".");                // "Hi, Charlie."

// 5. new keyword — this = new empty object
function Car(brand) {
  this.brand = brand; // this is the new object being created
}
const myCar = new Car("Toyota"); // myCar.brand = "Toyota"

// Priority order: new > bind > call/apply > method > function/global
```

---

## 10. Destructuring & Spread/Rest

### Array Destructuring

```javascript
const [a, b, c] = [1, 2, 3];
console.log(a, b, c); // 1 2 3

// Skip elements
const [first, , third] = [1, 2, 3];
console.log(first, third); // 1 3

// Default values
const [x = 10, y = 20] = [5];
console.log(x, y); // 5 20

// Rest pattern
const [head, ...tail] = [1, 2, 3, 4, 5];
console.log(head); // 1
console.log(tail); // [2, 3, 4, 5]

// Swap variables (elegant!)
let p = 1, q = 2;
[p, q] = [q, p];
console.log(p, q); // 2 1

// From function return
function getCoords() { return [10, 20]; }
const [lat, lng] = getCoords();
```

### Object Destructuring

```javascript
const person = { name: "Alice", age: 25, city: "NYC" };

// Basic
const { name, age } = person;
console.log(name, age); // Alice 25

// Rename while destructuring
const { name: userName, age: userAge } = person;
console.log(userName); // Alice

// Default values
const { name: n, salary = 50000 } = person;
console.log(salary); // 50000 (default, person doesn't have it)

// Rest in objects
const { name: personName, ...rest } = person;
console.log(rest); // { age: 25, city: "NYC" }

// Nested destructuring
const user = {
  id: 1,
  profile: {
    name: "Bob",
    address: {
      city: "LA",
      zip: "90001"
    }
  }
};

const { profile: { name: pName, address: { city } } } = user;
console.log(pName, city); // Bob LA

// In function parameters (very common in React!)
function greet({ name, age = 25, city = "Unknown" }) {
  return `${name} (${age}) from ${city}`;
}
greet({ name: "Alice", city: "NYC" }); // "Alice (25) from NYC"

// Array of objects
const users = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" },
];
const [{ name: firstName }] = users;
console.log(firstName); // Alice
```

---

## 11. Classes & Prototypes

### Prototype Chain

```javascript
// Everything in JS is linked through a prototype chain
// When you access a property, JS looks up the chain until found or null

const arr = [1, 2, 3];
// arr → Array.prototype → Object.prototype → null

arr.push(4);      // Found on Array.prototype
arr.toString();   // Found on Object.prototype
arr.hasOwnProperty("length"); // Found on Object.prototype

// You can see the prototype:
Object.getPrototypeOf(arr) === Array.prototype; // true

// Adding to prototype (extend all instances — use carefully!)
Array.prototype.sum = function() {
  return this.reduce((a, b) => a + b, 0);
};
[1,2,3].sum(); // 6
```

### ES6 Classes

```javascript
class Animal {
  // Class field (ES2022) — no need to declare in constructor
  #sound = "..."; // Private field with # prefix

  constructor(name, type) {
    this.name = name; // Public property
    this.type = type;
  }

  // Instance method
  speak() {
    return `${this.name} says ${this.#sound}`;
  }

  // Static method — called on class, not instances
  static create(name, type) {
    return new Animal(name, type);
  }

  // Getter
  get info() {
    return `${this.name} (${this.type})`;
  }

  // Setter
  set nickname(value) {
    if (typeof value !== "string") throw new Error("Must be a string");
    this._nickname = value;
  }
  get nickname() {
    return this._nickname ?? this.name;
  }
}

// Inheritance
class Dog extends Animal {
  #tricks = [];

  constructor(name) {
    super(name, "Dog"); // Must call super() first!
    this.#sound = "Woof"; // Private fields ARE inherited but... complex
  }

  learn(trick) {
    this.#tricks.push(trick);
  }

  // Override parent method
  speak() {
    return super.speak() + "!"; // Call parent's speak()
  }

  showTricks() {
    return `${this.name} knows: ${this.#tricks.join(", ")}`;
  }
}

const dog = new Dog("Buddy");
console.log(dog.speak());     // "Buddy says ... !" (or Woof with proper setup)
dog.learn("sit");
dog.learn("fetch");
console.log(dog.showTricks()); // "Buddy knows: sit, fetch"
console.log(dog instanceof Dog);    // true
console.log(dog instanceof Animal); // true

// Animal.create("Cat", "Feline"); // Static method call
```

---

## 12. Asynchronous JavaScript

### The Problem: JS is Single-Threaded

```
JS has ONE main thread. Long operations (network, file I/O) would BLOCK everything.
Solution: Async mechanisms — callbacks → Promises → async/await
```

### Callbacks (Old Way — "Callback Hell")

```javascript
// Simulating async with setTimeout
function fetchUser(id, callback) {
  setTimeout(() => {
    callback(null, { id, name: "Alice" }); // (error, data) convention
  }, 1000);
}

fetchUser(1, (err, user) => {
  if (err) { console.error(err); return; }
  fetchPosts(user.id, (err, posts) => {     // Nested!
    if (err) { console.error(err); return; }
    fetchComments(posts[0].id, (err, comments) => { // More nesting = Callback Hell!
      // ...
    });
  });
});
```

### Promises

```javascript
// A Promise is an object representing an eventual value
// States: pending → fulfilled (resolved) or rejected

// Creating a promise
const myPromise = new Promise((resolve, reject) => {
  const success = true;
  if (success) {
    resolve("Data loaded!"); // Fulfills the promise
  } else {
    reject(new Error("Something went wrong")); // Rejects the promise
  }
});

// Consuming a promise
myPromise
  .then(data => {
    console.log(data); // "Data loaded!"
    return data + " (processed)"; // Can return value for next .then()
  })
  .then(processedData => {
    console.log(processedData); // "Data loaded! (processed)"
  })
  .catch(error => {
    console.error(error.message); // Handles rejection from ANY previous step
  })
  .finally(() => {
    console.log("Always runs"); // Cleanup, loading state, etc.
  });

// Promise.all — waits for ALL promises (fails fast if any fails)
const p1 = fetch("/api/users");
const p2 = fetch("/api/posts");
const p3 = fetch("/api/comments");

Promise.all([p1, p2, p3])
  .then(([users, posts, comments]) => {
    // All three resolved
  })
  .catch(err => {
    // Triggered if ANY one fails
  });

// Promise.allSettled — waits for ALL, gives result of each (never rejects)
Promise.allSettled([p1, p2, p3]).then(results => {
  results.forEach(result => {
    if (result.status === "fulfilled") console.log(result.value);
    else console.log(result.reason);
  });
});

// Promise.race — resolves/rejects as soon as FIRST settles
Promise.race([p1, p2, p3]).then(firstResult => {
  // Whichever resolves/rejects first
});

// Promise.any — resolves when FIRST succeeds (rejects if all fail)
Promise.any([p1, p2, p3]).then(firstSuccess => {
  // First successful result
});
```

### async / await — The Modern Way

```javascript
// async/await is syntactic sugar over Promises — cleaner, more readable

// Basic usage
async function fetchData() {
  // await pauses execution until promise resolves
  const response = await fetch("https://api.example.com/data");
  const data = await response.json();
  return data; // async functions always return a Promise
}

// Error handling with try/catch
async function getUser(id) {
  try {
    const res = await fetch(`/api/users/${id}`);

    if (!res.ok) {
      throw new Error(`HTTP ${res.status}`);
    }

    const user = await res.json();
    return user;
  } catch (error) {
    console.error("Failed to fetch user:", error.message);
    throw error; // Re-throw if caller needs to handle it
  } finally {
    console.log("Fetch attempt complete");
  }
}

// Parallel requests (don't await individually — they'd run sequentially!)
async function getAll() {
  // ❌ Sequential (slow — each waits for previous)
  const user    = await fetch("/api/user");
  const posts   = await fetch("/api/posts");
  const comments = await fetch("/api/comments");

  // ✅ Parallel (fast — all start simultaneously)
  const [user2, posts2, comments2] = await Promise.all([
    fetch("/api/user"),
    fetch("/api/posts"),
    fetch("/api/comments")
  ]);
}

// Async in different contexts
// 1. Async arrow function
const loadData = async () => {
  const data = await fetchSomething();
  return data;
};

// 2. Async IIFE (when top-level await not available)
(async () => {
  const result = await loadData();
  console.log(result);
})();

// 3. Async class method
class Api {
  async getUser(id) {
    return await fetch(`/api/users/${id}`).then(r => r.json());
  }
}

// For-await-of — async iteration
async function processStream(stream) {
  for await (const chunk of stream) {
    process(chunk);
  }
}
```

### Fetch API

```javascript
// GET request
const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
const post = await response.json();

// POST request
const res = await fetch("/api/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Authorization": `Bearer ${token}`
  },
  body: JSON.stringify({ name: "Alice", email: "alice@example.com" })
});

const newUser = await res.json();

// Error handling — fetch doesn't throw on HTTP errors!
const response2 = await fetch("/api/data");
if (!response2.ok) {
  throw new Error(`HTTP error! Status: ${response2.status}`);
}

// Full robust fetch wrapper
async function apiRequest(url, options = {}) {
  const defaults = {
    headers: { "Content-Type": "application/json" }
  };
  const config = { ...defaults, ...options };

  const response = await fetch(url, config);

  if (!response.ok) {
    const error = await response.json().catch(() => ({}));
    throw new Error(error.message || `HTTP ${response.status}`);
  }

  return response.json();
}
```

---

## 13. ES6+ Modern Features

### Template Literals

```javascript
const name = "Alice";
const age = 25;

// Multi-line strings
const message = `
  Hello, ${name}!
  You are ${age} years old.
  Next year you'll be ${age + 1}.
`;

// Tagged template literals
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) => {
    return result + str + (values[i] ? `<strong>${values[i]}</strong>` : "");
  }, "");
}
const output = highlight`Hello ${name}, you are ${age} years old.`;
// "Hello <strong>Alice</strong>, you are <strong>25</strong> years old."
```

### Symbols

```javascript
const sym1 = Symbol("description");
const sym2 = Symbol("description");
sym1 === sym2; // false — always unique

// Use case: unique object keys (won't clash with other properties)
const ID = Symbol("id");
const obj = { [ID]: 123, name: "Alice" };
obj[ID];   // 123
// Won't appear in for...in or Object.keys()

// Well-known symbols
class MyIterable {
  [Symbol.iterator]() { // Makes object iterable!
    let i = 0;
    return {
      next() {
        return i < 3 ? { value: i++, done: false } : { done: true };
      }
    };
  }
}
for (const val of new MyIterable()) {
  console.log(val); // 0 1 2
}
```

### Map and Set

```javascript
// MAP — key-value pairs where keys can be ANY type
const map = new Map();
map.set("name", "Alice");
map.set(42, "the answer");
map.set({ id: 1 }, "user object key");

map.get("name");    // "Alice"
map.has("name");    // true
map.size;           // 3
map.delete("name"); // true
map.clear();        // empties the map

// Iterate
for (const [key, value] of map) {
  console.log(key, value);
}
map.forEach((value, key) => console.log(key, value));

// Convert to array
[...map.keys()];    // all keys
[...map.values()];  // all values
[...map.entries()]; // all [key, value] pairs

// Object vs Map
// - Map keys can be ANY type; Object keys are always strings/symbols
// - Map maintains insertion order
// - Map has .size; Objects need Object.keys().length
// - Map is better for frequent add/remove operations

// SET — unique values only
const set = new Set([1, 2, 2, 3, 3, 3]); // Set {1, 2, 3}
set.add(4);         // Set {1, 2, 3, 4}
set.has(2);         // true
set.delete(2);      // true
set.size;           // 3

// Remove duplicates from array!
const unique = [...new Set([1, 2, 2, 3, 3])]; // [1, 2, 3]

// Set operations
const a = new Set([1, 2, 3, 4]);
const b = new Set([3, 4, 5, 6]);

// Union
const union = new Set([...a, ...b]); // {1,2,3,4,5,6}

// Intersection
const intersection = new Set([...a].filter(x => b.has(x))); // {3,4}

// Difference
const difference = new Set([...a].filter(x => !b.has(x))); // {1,2}
```

### Generators

```javascript
// Generators are functions that can pause and resume!
function* counter() {
  let i = 0;
  while (true) {
    yield i++; // Pauses here, returns i, resumes on next .next() call
  }
}

const gen = counter();
gen.next(); // { value: 0, done: false }
gen.next(); // { value: 1, done: false }
gen.next(); // { value: 2, done: false }

// Finite generator
function* range(start, end, step = 1) {
  for (let i = start; i < end; i += step) {
    yield i;
  }
}

for (const num of range(0, 10, 2)) {
  console.log(num); // 0 2 4 6 8
}

[...range(1, 5)]; // [1, 2, 3, 4]
```

### WeakMap & WeakRef (For Memory Management)

```javascript
// WeakMap — keys must be objects, allows garbage collection
const weakMap = new WeakMap();
let obj = { name: "Alice" };
weakMap.set(obj, "some data");
obj = null; // obj can now be garbage collected, weakMap won't prevent it

// Use case: storing private data for objects
const _private = new WeakMap();
class Person {
  constructor(name, age) {
    _private.set(this, { age }); // Store private data
    this.name = name;
  }
  getAge() { return _private.get(this).age; }
}
```

---

## 14. DOM Manipulation

### Selecting Elements

```javascript
// By ID (returns single element or null)
const el = document.getElementById("myId");

// CSS selector — single (first match)
const el2 = document.querySelector(".myClass");
const el3 = document.querySelector("#id .class > p");

// CSS selector — all matches (NodeList)
const all = document.querySelectorAll("p.highlight");

// Convert NodeList to Array for full array methods
const arr = Array.from(all); // or [...all]

// Other selectors (legacy but still used)
document.getElementsByClassName("myClass"); // HTMLCollection
document.getElementsByTagName("div");       // HTMLCollection
document.getElementsByName("email");         // NodeList
```

### Manipulating Elements

```javascript
const el = document.querySelector("#myEl");

// Content
el.textContent = "Plain text (safe — no HTML parsing)";
el.innerHTML = "<strong>Bold</strong>"; // ⚠️ XSS risk with user data!
el.innerText = "Respects CSS visibility";

// Attributes
el.getAttribute("href");
el.setAttribute("href", "https://example.com");
el.removeAttribute("disabled");
el.hasAttribute("readonly");

// Data attributes
// <div data-user-id="42" data-role="admin">
el.dataset.userId; // "42" (camelCase conversion)
el.dataset.role;   // "admin"

// Classes
el.classList.add("active", "highlight");
el.classList.remove("hidden");
el.classList.toggle("visible");      // Add if absent, remove if present
el.classList.contains("active");     // true/false
el.classList.replace("old", "new");  // Replace class
el.className;                        // All classes as string

// Styles
el.style.color = "red";
el.style.backgroundColor = "blue";  // camelCase!
el.style.display = "none";          // Hide
el.style.cssText = "color:red; font-size:16px"; // Multiple at once
window.getComputedStyle(el).color;  // Get actual computed style
```

### Creating & Removing Elements

```javascript
// Creating
const newDiv = document.createElement("div");
newDiv.textContent = "Hello!";
newDiv.className = "card";
newDiv.setAttribute("id", "myCard");

// Inserting
document.body.appendChild(newDiv);       // Append at end
parent.insertBefore(newDiv, sibling);    // Before a sibling

// Modern insertion methods
parent.prepend(newDiv);                  // First child
parent.append(newDiv, "text", otherEl); // Last child (multiple)
sibling.before(newDiv);                 // Before sibling
sibling.after(newDiv);                  // After sibling

// insertAdjacentHTML — fast HTML insertion
el.insertAdjacentHTML("beforeend", "<p>Added!</p>");
// Positions: 'beforebegin', 'afterbegin', 'beforeend', 'afterend'

// Removing
el.remove();                      // Modern — remove itself
parent.removeChild(child);        // Old way

// Cloning
const clone = el.cloneNode(true); // true = deep clone (with children)

// Document Fragment — batch DOM operations for performance
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
  const li = document.createElement("li");
  li.textContent = `Item ${i}`;
  fragment.appendChild(li); // Build in memory
}
list.appendChild(fragment); // One DOM update instead of 1000!
```

---

## 15. Events & Event Loop

### Event Listeners

```javascript
const btn = document.querySelector("#myBtn");

// addEventListener (preferred)
function handleClick(event) {
  console.log("Clicked!", event.target);
  event.preventDefault();  // Prevent default behavior (form submit, link navigate)
  event.stopPropagation(); // Stop event from bubbling up
}

btn.addEventListener("click", handleClick);
btn.removeEventListener("click", handleClick); // Must use same reference!

// Arrow function (can't remove — no reference)
btn.addEventListener("click", (e) => console.log(e));

// Options
btn.addEventListener("click", handler, { once: true }); // Fires once then removes
btn.addEventListener("click", handler, { capture: true }); // Capture phase

// Common Events
// Mouse: click, dblclick, mousedown, mouseup, mouseover, mouseout, mousemove
// Keyboard: keydown, keyup, keypress
// Form: submit, change, input, focus, blur, reset
// Window: load, DOMContentLoaded, resize, scroll, beforeunload
// Touch: touchstart, touchmove, touchend
```

### Event Bubbling & Delegation

```javascript
// Events bubble up from child to parent to document
// <div id="parent"> <button id="child"> Click </button> </div>

document.querySelector("#child").addEventListener("click", () => {
  console.log("1. Child clicked");
});
document.querySelector("#parent").addEventListener("click", () => {
  console.log("2. Parent notified (bubbled up)");
});

// Event Delegation — attach one listener to parent, handle multiple children
// Instead of adding listener to each <li>, add ONE to <ul>
document.querySelector("ul").addEventListener("click", (event) => {
  // event.target = the actual element clicked
  if (event.target.matches("li")) {
    console.log("List item clicked:", event.target.textContent);
  }
  if (event.target.closest(".delete-btn")) {
    // Handle delete
  }
});
// Works even for dynamically added <li> elements!
```

### The Event Loop — How Async JS Works

```javascript
// JS has ONE call stack (single-threaded)
// Async tasks go to Web APIs, then to Queue, then back to Stack

// Execution order:
console.log("1. Sync");           // 1. Runs immediately

setTimeout(() => {
  console.log("3. Macro-task");   // 3. After ALL sync + microtasks
}, 0);

Promise.resolve().then(() => {
  console.log("2. Micro-task");   // 2. After current sync, before macro-tasks
});

console.log("1b. Also Sync");     // 1b. Runs immediately

// Output order: 1. Sync → 1b. Also Sync → 2. Micro-task → 3. Macro-task

// Microtasks (higher priority, drain completely before macro):
// - Promise .then/.catch/.finally
// - queueMicrotask()
// - MutationObserver

// Macrotasks (one at a time, per event loop tick):
// - setTimeout, setInterval
// - setImmediate (Node.js)
// - I/O, UI rendering, user events
```

---

## 16. Error Handling

### try / catch / finally

```javascript
function parseJSON(str) {
  try {
    const data = JSON.parse(str);
    return data;
  } catch (error) {
    if (error instanceof SyntaxError) {
      console.error("Invalid JSON:", error.message);
    } else {
      throw error; // Re-throw unexpected errors
    }
    return null;
  } finally {
    console.log("Parsing attempt complete"); // Always runs
  }
}

// Custom Errors
class ValidationError extends Error {
  constructor(message, field) {
    super(message);
    this.name = "ValidationError";
    this.field = field;
  }
}

class NetworkError extends Error {
  constructor(status, url) {
    super(`HTTP ${status} from ${url}`);
    this.name = "NetworkError";
    this.status = status;
  }
}

function validateEmail(email) {
  if (!email.includes("@")) {
    throw new ValidationError("Invalid email format", "email");
  }
}

try {
  validateEmail("notanemail");
} catch (e) {
  if (e instanceof ValidationError) {
    console.log(`Validation error on field '${e.field}': ${e.message}`);
  }
}

// Global error handling
window.onerror = (message, source, line, col, error) => {
  console.log("Global error:", error);
};

window.addEventListener("unhandledrejection", (event) => {
  console.error("Unhandled promise rejection:", event.reason);
  event.preventDefault();
});
```

---

## 17. Modules (ESM)

```javascript
// math.js — Named exports
export const PI = 3.14159;
export function add(a, b) { return a + b; }
export function subtract(a, b) { return a - b; }

// utils.js — Default export (one per file)
export default function formatDate(date) {
  return date.toLocaleDateString();
}

// Also works:
const helper = () => {};
export { helper };         // Named export after definition
export { helper as util }; // Export with alias

// main.js — Importing
import formatDate from "./utils.js";          // Default import
import { add, PI } from "./math.js";          // Named imports
import { add as sum } from "./math.js";       // Named with alias
import * as MathUtils from "./math.js";       // Import all as namespace
import formatDate, { add } from "./module";   // Mix default + named

// Dynamic imports (lazy loading)
const module = await import("./heavy-module.js");
module.doSomething();

// Or with then
import("./module.js").then(m => m.default());

// Re-exporting
export { add } from "./math.js";           // Re-export named
export { default } from "./utils.js";      // Re-export default
export * from "./math.js";                 // Re-export all
```

---

## 18. JS Design Patterns

### Singleton

```javascript
class DatabaseConnection {
  static #instance = null;

  #connection;

  constructor(url) {
    if (DatabaseConnection.#instance) {
      return DatabaseConnection.#instance; // Return existing instance
    }
    this.#connection = connect(url);
    DatabaseConnection.#instance = this;
  }

  static getInstance(url) {
    if (!this.#instance) {
      this.#instance = new DatabaseConnection(url);
    }
    return this.#instance;
  }
}

const db1 = DatabaseConnection.getInstance("mongodb://...");
const db2 = DatabaseConnection.getInstance("mongodb://...");
console.log(db1 === db2); // true — same instance!
```

### Observer / Pub-Sub

```javascript
class EventEmitter {
  #listeners = new Map();

  on(event, listener) {
    if (!this.#listeners.has(event)) {
      this.#listeners.set(event, []);
    }
    this.#listeners.get(event).push(listener);
    return () => this.off(event, listener); // Returns unsubscribe function
  }

  off(event, listener) {
    const listeners = this.#listeners.get(event) || [];
    this.#listeners.set(event, listeners.filter(l => l !== listener));
  }

  emit(event, ...args) {
    (this.#listeners.get(event) || []).forEach(listener => listener(...args));
  }
}

const emitter = new EventEmitter();
const unsubscribe = emitter.on("data", (data) => console.log(data));
emitter.emit("data", { id: 1, name: "Alice" }); // Logs the data
unsubscribe(); // Stop listening
```

### Factory

```javascript
function createAnimal(type, name) {
  const animals = {
    dog: { sound: "Woof", legs: 4 },
    cat: { sound: "Meow", legs: 4 },
    bird: { sound: "Tweet", legs: 2 },
  };

  if (!animals[type]) throw new Error(`Unknown animal: ${type}`);

  return {
    name,
    type,
    ...animals[type],
    speak() { return `${this.name} says ${this.sound}`; }
  };
}

const dog = createAnimal("dog", "Buddy");
dog.speak(); // "Buddy says Woof"
```

---

# PART 2 — REACT

---

## 19. React Core Concepts

### What is React?

React is a **JavaScript library** (not framework!) for building user interfaces. Created by Facebook/Meta.

**Key Ideas:**
1. **Component-Based** — UI split into reusable pieces
2. **Declarative** — Describe WHAT the UI should look like, React figures out HOW
3. **Virtual DOM** — React's in-memory representation of the real DOM
4. **Unidirectional Data Flow** — Data flows down (parent → child)

### How React Works

```
State/Props Change
      ↓
React re-renders component (creates new Virtual DOM tree)
      ↓
Diffing Algorithm compares new vs old Virtual DOM
      ↓
Only the CHANGED parts are updated in the real DOM (reconciliation)
      ↓
Efficient, fast UI updates!
```

### React vs Vanilla JS

```javascript
// Vanilla JS — Imperative: tell it HOW to do it
const btn = document.querySelector("button");
const counter = document.querySelector("#count");
let count = 0;
btn.addEventListener("click", () => {
  count++;
  counter.textContent = count;
});

// React — Declarative: tell it WHAT you want
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
// React handles DOM updates automatically!
```

---

## 20. JSX

JSX = JavaScript XML. It lets you write HTML-like syntax in JavaScript.

```jsx
// JSX is compiled to React.createElement() calls
const element = <h1>Hello World</h1>;

// Compiles to:
const element = React.createElement("h1", null, "Hello World");

// With props:
const btn = <button className="btn" onClick={handler}>Click</button>;
// Compiles to:
const btn = React.createElement("button", { className: "btn", onClick: handler }, "Click");
```

### JSX Rules

```jsx
// 1. Must return SINGLE root element
// ❌ Wrong
return (
  <h1>Title</h1>
  <p>Para</p>
);

// ✅ Correct — wrap in div or Fragment
return (
  <div>
    <h1>Title</h1>
    <p>Para</p>
  </div>
);

// ✅ Better — use Fragment (no extra DOM node)
return (
  <>
    <h1>Title</h1>
    <p>Para</p>
  </>
);
// <> </> is shorthand for <React.Fragment> </React.Fragment>

// 2. All tags must be closed
// ❌ <br>  <input>  <img>
// ✅ <br/> <input/> <img/>

// 3. Use className instead of class
<div className="container">  {/* Not class="container" */}

// 4. Use htmlFor instead of for (in labels)
<label htmlFor="email">Email</label>

// 5. JavaScript expressions in curly braces {}
const name = "Alice";
const jsx = (
  <h1>Hello, {name}!</h1>           // Variable
  <p>{2 + 2}</p>                    // Expression
  <p>{isLoggedIn ? "Hi" : "Login"}</p> // Ternary
  <p>{items.length > 0 && <List />}</p> // Short-circuit
);

// 6. Styling
<div style={{ color: "red", fontSize: "16px" }}>
  {/* Note: double braces — outer {} for JS, inner {} for object */}

// 7. Comments in JSX
<div>
  {/* This is a JSX comment */}
</div>

// 8. Lists need KEY prop
const list = items.map(item =>
  <li key={item.id}>{item.name}</li> // key must be unique & stable
);
```

---

## 21. Components — Functional & Class

### Functional Components (Modern — Preferred)

```jsx
// Simplest component
function Hello() {
  return <h1>Hello World!</h1>;
}

// Arrow function component
const Hello = () => <h1>Hello World!</h1>;

// With props
function Greeting({ name, age = 25 }) { // Destructure props
  return (
    <div>
      <h1>Hello, {name}!</h1>
      <p>Age: {age}</p>
    </div>
  );
}

// Usage
<Greeting name="Alice" />
<Greeting name="Bob" age={30} />
```

### Class Components (Legacy — Know for interviews)

```jsx
import React, { Component } from "react";

class Counter extends Component {
  // State
  state = { count: 0 };

  // Or in constructor:
  constructor(props) {
    super(props); // MUST call super(props) first!
    this.state = { count: 0 };
    this.handleClick = this.handleClick.bind(this); // Bind methods!
  }

  handleClick() {
    this.setState({ count: this.state.count + 1 });
    // setState with callback (safe for prev state)
    this.setState(prevState => ({ count: prevState.count + 1 }));
  }

  // Lifecycle methods
  componentDidMount() {
    // Runs after first render — fetch data, set up subscriptions
    document.title = `Count: ${this.state.count}`;
  }

  componentDidUpdate(prevProps, prevState) {
    // Runs after every update
    if (prevState.count !== this.state.count) {
      document.title = `Count: ${this.state.count}`;
    }
  }

  componentWillUnmount() {
    // Cleanup — clear intervals, unsubscribe
    clearInterval(this.timer);
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    );
  }
}
```

---

## 22. Props

### Passing Props

```jsx
// Parent passes props like HTML attributes
function App() {
  const user = { name: "Alice", age: 25 };

  return (
    <UserCard
      name={user.name}
      age={user.age}
      isAdmin={true}
      onClick={() => alert("clicked")}
      user={user}          // Can pass objects
      children={<p>Hi</p>} // Can pass JSX (but use children prop normally)
    />
  );
}

// Child receives as object (conventionally named 'props')
function UserCard(props) {
  return <div>{props.name} - {props.age}</div>;
}

// Destructure for cleaner code
function UserCard({ name, age, isAdmin = false, onClick }) {
  return (
    <div onClick={onClick}>
      <h2>{name} {isAdmin && "⭐ Admin"}</h2>
      <p>Age: {age}</p>
    </div>
  );
}

// Spread props
function Button({ className, ...rest }) {
  return <button className={`btn ${className}`} {...rest} />;
}
<Button className="primary" onClick={fn} disabled={false} />
```

### Children Prop

```jsx
// Anything between component tags = children
function Card({ title, children }) {
  return (
    <div className="card">
      <h2>{title}</h2>
      <div className="card-body">
        {children}
      </div>
    </div>
  );
}

// Usage
<Card title="My Card">
  <p>This is the card content</p>
  <button>Click me</button>
</Card>
```

### PropTypes (Runtime Type Checking)

```jsx
import PropTypes from "prop-types";

function UserCard({ name, age, email, role }) {
  return <div>{name}</div>;
}

UserCard.propTypes = {
  name:  PropTypes.string.isRequired,
  age:   PropTypes.number,
  email: PropTypes.string,
  role:  PropTypes.oneOf(["admin", "user", "moderator"]),
  user:  PropTypes.shape({
    id:   PropTypes.number.isRequired,
    name: PropTypes.string,
  }),
  children: PropTypes.node,
  onClick:  PropTypes.func,
};

UserCard.defaultProps = {
  age:  25,
  role: "user",
};
```

---

## 23. State & useState

```jsx
import { useState } from "react";

// useState returns [currentValue, setterFunction]
function Counter() {
  const [count, setCount] = useState(0); // Initial value is 0

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
      <button onClick={() => setCount(count - 1)}>-</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}

// IMPORTANT RULES:
// 1. Always use setter function, NEVER mutate state directly
// ❌ count++; state.name = "Bob"; state.items.push(x);
// ✅ setCount(count + 1); setName("Bob"); setItems([...items, x]);

// 2. Use functional update form when new state depends on old state
setCount(prevCount => prevCount + 1); // SAFE in concurrent mode
// Not: setCount(count + 1);  // Could use stale value

// 3. State updates are BATCHED (in React 18+, even in async code)

// Object state
function UserForm() {
  const [user, setUser] = useState({ name: "", email: "", age: 0 });

  const updateField = (field, value) => {
    setUser(prev => ({
      ...prev,           // Keep all other fields
      [field]: value     // Update only this field
    }));
  };

  return (
    <input
      value={user.name}
      onChange={e => updateField("name", e.target.value)}
    />
  );
}

// Array state
function TodoList() {
  const [todos, setTodos] = useState([]);

  const addTodo = (text) => {
    setTodos(prev => [...prev, { id: Date.now(), text, done: false }]);
  };

  const toggleTodo = (id) => {
    setTodos(prev =>
      prev.map(todo =>
        todo.id === id ? { ...todo, done: !todo.done } : todo
      )
    );
  };

  const deleteTodo = (id) => {
    setTodos(prev => prev.filter(todo => todo.id !== id));
  };
}

// Lazy initialization (for expensive computation)
const [state, setState] = useState(() => {
  const value = computeExpensiveValue(); // Only runs once
  return value;
});
```

---

## 24. useEffect Hook

```jsx
import { useEffect, useState } from "react";

// useEffect(callback, dependencyArray)

// 1. Runs AFTER EVERY render (no dependency array)
useEffect(() => {
  console.log("After every render");
});

// 2. Runs ONCE after first render (empty dependency array)
useEffect(() => {
  console.log("After mount only");
  // Great for: API calls, setting up subscriptions
}, []);

// 3. Runs when specific values change
useEffect(() => {
  console.log("count changed:", count);
  document.title = `Count: ${count}`;
}, [count]); // Only runs when 'count' changes

// 4. Cleanup function (returned from effect)
useEffect(() => {
  const timer = setInterval(() => {
    setCount(c => c + 1);
  }, 1000);

  // Cleanup runs BEFORE next effect OR when component unmounts
  return () => clearInterval(timer);
}, []); // Set up once, clean up on unmount

// Real-world: Fetching data
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    let cancelled = false; // Handle race conditions

    const fetchUser = async () => {
      try {
        setLoading(true);
        setError(null);
        const res = await fetch(`/api/users/${userId}`);
        if (!res.ok) throw new Error(`HTTP ${res.status}`);
        const data = await res.json();
        if (!cancelled) setUser(data); // Only update if still mounted
      } catch (err) {
        if (!cancelled) setError(err.message);
      } finally {
        if (!cancelled) setLoading(false);
      }
    };

    fetchUser();

    return () => { cancelled = true; }; // Cleanup
  }, [userId]); // Re-fetch when userId changes

  if (loading) return <Spinner />;
  if (error)   return <Error message={error} />;
  return <div>{user.name}</div>;
}

// COMMON MISTAKE: Infinite loop
// ❌ This causes infinite loop!
useEffect(() => {
  setData(processData()); // Updating state inside effect
}, [data]);               // with data as dependency = infinite!

// ✅ Fix: exclude data if it's set inside the effect
useEffect(() => {
  setData(processData(inputValue)); // Only depend on input
}, [inputValue]);
```

---

## 25. All React Hooks

### useReducer — Complex State Logic

```jsx
import { useReducer } from "react";

// Like Redux but local to component
// Best when: multiple related state values, complex update logic

const initialState = { count: 0, step: 1, error: null };

function counterReducer(state, action) {
  switch (action.type) {
    case "INCREMENT":
      return { ...state, count: state.count + state.step };
    case "DECREMENT":
      return { ...state, count: state.count - state.step };
    case "SET_STEP":
      return { ...state, step: action.payload };
    case "RESET":
      return initialState;
    default:
      throw new Error(`Unknown action: ${action.type}`);
  }
}

function Counter() {
  const [state, dispatch] = useReducer(counterReducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>+</button>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>-</button>
      <button onClick={() => dispatch({ type: "SET_STEP", payload: 5 })}>
        Set Step to 5
      </button>
      <button onClick={() => dispatch({ type: "RESET" })}>Reset</button>
    </div>
  );
}
```

### useRef — Persist Values Without Re-render

```jsx
import { useRef, useEffect } from "react";

function TextInput() {
  // 1. DOM Reference — access DOM elements directly
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus(); // Direct DOM access
    inputRef.current.select(); // Select all text
  };

  // 2. Mutable value — survives re-renders, doesn't CAUSE re-renders
  const renderCount = useRef(0);
  const previousCount = useRef(0);

  useEffect(() => {
    renderCount.current += 1; // Doesn't trigger re-render
    previousCount.current = count;
  });

  // 3. Store timer IDs, subscriptions, etc.
  const timerRef = useRef(null);

  const startTimer = () => {
    timerRef.current = setInterval(() => {
      // ...
    }, 1000);
  };

  const stopTimer = () => {
    clearInterval(timerRef.current);
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus</button>
    </div>
  );
}
```

### useMemo — Memoize Expensive Computations

```jsx
import { useMemo, useState } from "react";

function ExpensiveList({ items, filter }) {
  // Only recalculates when items or filter changes
  const filteredItems = useMemo(() => {
    console.log("Filtering...");
    return items.filter(item =>
      item.name.toLowerCase().includes(filter.toLowerCase())
    );
  }, [items, filter]); // Dependencies

  // Without useMemo: recalculates on EVERY render (even unrelated state changes)

  return <ul>{filteredItems.map(item => <li key={item.id}>{item.name}</li>)}</ul>;
}
```

### useCallback — Memoize Functions

```jsx
import { useCallback, useState } from "react";

// Functions are recreated on every render
// If passed as props, child re-renders every time (even with React.memo)
// useCallback memoizes the function

function Parent() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState("");

  // Without useCallback: new function every render → Child always re-renders
  // With useCallback: same function reference → Child only re-renders when count changes
  const handleClick = useCallback(() => {
    console.log("Count is:", count);
    setCount(c => c + 1);
  }, [count]); // Only recreate when count changes

  return (
    <div>
      <input value={name} onChange={e => setName(e.target.value)} />
      <Child onClick={handleClick} />
    </div>
  );
}

const Child = React.memo(({ onClick }) => {
  console.log("Child rendered");
  return <button onClick={onClick}>Click</button>;
}); // React.memo prevents re-render if props didn't change
```

### useContext — Consume Context

```jsx
const ThemeContext = createContext("light");

function ThemedButton() {
  const theme = useContext(ThemeContext); // No Consumer wrapper needed
  return <button className={theme}>Themed Button</button>;
}
// (Context setup covered in Section 26)
```

### useLayoutEffect — Like useEffect but Synchronous

```jsx
import { useLayoutEffect, useRef } from "react";

// Fires SYNCHRONOUSLY after DOM mutations but BEFORE browser paint
// Use when: measuring DOM, preventing visual flash

function Tooltip({ text, anchor }) {
  const tooltipRef = useRef(null);

  useLayoutEffect(() => {
    // Measure and position BEFORE user sees anything
    const { height } = tooltipRef.current.getBoundingClientRect();
    tooltipRef.current.style.top = `${anchor.y - height}px`;
  }, [anchor]);

  return <div ref={tooltipRef} className="tooltip">{text}</div>;
}

// useEffect vs useLayoutEffect:
// useEffect:       Paint → Effect  (user might see flash)
// useLayoutEffect: Effect → Paint  (blocks paint, no flash, but blocks!)
// Use useLayoutEffect ONLY when you need to measure/mutate DOM before paint
```

### useId — Generate Unique IDs (React 18)

```jsx
import { useId } from "react";

function FormField({ label }) {
  const id = useId(); // Generates unique, stable ID

  return (
    <div>
      <label htmlFor={id}>{label}</label>
      <input id={id} type="text" />
    </div>
  );
}
// Multiple FormField instances get unique IDs
// Safe for server-side rendering too
```

### useTransition — Non-Urgent Updates (React 18)

```jsx
import { useTransition, useState } from "react";

function SearchResults() {
  const [isPending, startTransition] = useTransition();
  const [query, setQuery] = useState("");
  const [results, setResults] = useState([]);

  const handleSearch = (e) => {
    setQuery(e.target.value); // Urgent: update input immediately

    startTransition(() => {
      // Non-urgent: can be interrupted
      setResults(searchDatabase(e.target.value)); // Expensive operation
    });
  };

  return (
    <div>
      <input onChange={handleSearch} value={query} />
      {isPending ? <Spinner /> : <ResultsList results={results} />}
    </div>
  );
}
```

### useDeferredValue — Defer Expensive Renders (React 18)

```jsx
import { useDeferredValue, useState } from "react";

function Search({ query }) {
  const deferredQuery = useDeferredValue(query); // Lags behind during typing

  // This expensive component only re-renders with the deferred (lagged) value
  // Input stays responsive, results update when browser is free
  return <ExpensiveSearchResults query={deferredQuery} />;
}
```

---

## 26. Context API

Context solves **prop drilling** — passing props through many levels.

```jsx
import { createContext, useContext, useState, useReducer } from "react";

// Step 1: Create Context
const AuthContext = createContext(null);

// Step 2: Create Provider Component
function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  const login = async (email, password) => {
    const data = await loginAPI(email, password);
    setUser(data.user);
  };

  const logout = () => {
    setUser(null);
  };

  const value = { user, login, logout, isLoggedIn: !!user };

  return (
    <AuthContext.Provider value={value}>
      {children}
    </AuthContext.Provider>
  );
}

// Step 3: Custom hook for consuming (best practice)
function useAuth() {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error("useAuth must be used within AuthProvider");
  }
  return context;
}

// Step 4: Wrap app with Provider
function App() {
  return (
    <AuthProvider>
      <Router />
    </AuthProvider>
  );
}

// Step 5: Consume anywhere in the tree
function NavBar() {
  const { user, logout, isLoggedIn } = useAuth();

  return (
    <nav>
      {isLoggedIn ? (
        <>
          <span>Hello, {user.name}!</span>
          <button onClick={logout}>Logout</button>
        </>
      ) : (
        <Link to="/login">Login</Link>
      )}
    </nav>
  );
}

// Multiple contexts
const ThemeContext = createContext("light");
const LanguageContext = createContext("en");

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <LanguageContext.Provider value="hi">
        <App />
      </LanguageContext.Provider>
    </ThemeContext.Provider>
  );
}
```

---

## 27. React Router

```jsx
// npm install react-router-dom

import {
  BrowserRouter,
  Routes,
  Route,
  Link,
  NavLink,
  useNavigate,
  useParams,
  useLocation,
  useSearchParams,
  Outlet,
  Navigate,
} from "react-router-dom";

// Setup
function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/"        element={<Home />} />
        <Route path="/about"   element={<About />} />
        <Route path="/users"   element={<UsersLayout />}>
          <Route index          element={<UsersList />} />   {/* /users */}
          <Route path=":id"     element={<UserDetail />} />  {/* /users/123 */}
          <Route path=":id/edit" element={<UserEdit />} />   {/* /users/123/edit */}
        </Route>
        <Route path="*"        element={<NotFound />} />    {/* 404 */}
      </Routes>
    </BrowserRouter>
  );
}

// Nested route parent — must include <Outlet />
function UsersLayout() {
  return (
    <div>
      <h1>Users Section</h1>
      <Outlet /> {/* Child routes render here */}
    </div>
  );
}

// Navigation links
function Navigation() {
  return (
    <nav>
      <Link to="/">Home</Link>                   {/* Basic link */}
      <NavLink
        to="/about"
        className={({ isActive }) => isActive ? "active" : ""}
      >
        About
      </NavLink>
    </nav>
  );
}

// Reading URL parameters
function UserDetail() {
  const { id } = useParams();          // /users/123 → id = "123"
  return <div>User ID: {id}</div>;
}

// Programmatic navigation
function LoginForm() {
  const navigate = useNavigate();

  const handleSubmit = async () => {
    await login();
    navigate("/dashboard");           // Go to dashboard
    navigate(-1);                     // Go back
    navigate("/login", { replace: true }); // Replace history entry
  };
}

// Query parameters  (/search?q=react&page=2)
function SearchPage() {
  const [searchParams, setSearchParams] = useSearchParams();
  const query = searchParams.get("q") || "";
  const page  = Number(searchParams.get("page")) || 1;

  const handleSearch = (newQuery) => {
    setSearchParams({ q: newQuery, page: 1 });
  };
}

// Location
function AnyComponent() {
  const location = useLocation();
  console.log(location.pathname); // /users/123
  console.log(location.search);   // ?page=2
  console.log(location.state);    // State passed via navigate
}

// Protected Routes
function ProtectedRoute({ children }) {
  const { isLoggedIn } = useAuth();
  return isLoggedIn
    ? children
    : <Navigate to="/login" replace />;
}

// Usage
<Route path="/dashboard" element={
  <ProtectedRoute>
    <Dashboard />
  </ProtectedRoute>
} />
```

---

## 28. State Management (Redux / Zustand)

### Redux Toolkit (Modern Redux)

```jsx
// npm install @reduxjs/toolkit react-redux

// store/slices/counterSlice.js
import { createSlice, createAsyncThunk } from "@reduxjs/toolkit";

// Async action (thunk)
export const fetchUsers = createAsyncThunk(
  "users/fetchAll",
  async (_, { rejectWithValue }) => {
    try {
      const res = await fetch("/api/users");
      return await res.json();
    } catch (err) {
      return rejectWithValue(err.message);
    }
  }
);

const counterSlice = createSlice({
  name: "counter",
  initialState: { value: 0, status: "idle" },
  reducers: {
    increment: (state) => { state.value += 1; }, // Immer makes mutation safe!
    decrement: (state) => { state.value -= 1; },
    incrementBy: (state, action) => { state.value += action.payload; },
    reset: (state) => { state.value = 0; },
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchUsers.pending,   (state) => { state.status = "loading"; })
      .addCase(fetchUsers.fulfilled, (state, action) => {
        state.status = "succeeded";
        state.users = action.payload;
      })
      .addCase(fetchUsers.rejected,  (state, action) => {
        state.status = "failed";
        state.error = action.payload;
      });
  }
});

export const { increment, decrement, incrementBy, reset } = counterSlice.actions;
export default counterSlice.reducer;

// store/index.js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./slices/counterSlice";

const store = configureStore({
  reducer: {
    counter: counterReducer,
    // Add more slices here
  }
});

export default store;

// main.jsx
import { Provider } from "react-redux";
<Provider store={store}>
  <App />
</Provider>

// Component usage
import { useSelector, useDispatch } from "react-redux";

function Counter() {
  const count    = useSelector(state => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => dispatch(increment())}>+</button>
      <button onClick={() => dispatch(incrementBy(5))}>+5</button>
    </div>
  );
}
```

### Zustand (Simpler Alternative)

```jsx
// npm install zustand

import { create } from "zustand";

const useStore = create((set, get) => ({
  // State
  count: 0,
  bears: 0,
  user: null,

  // Actions
  increment: () => set(state => ({ count: state.count + 1 })),
  decrement: () => set(state => ({ count: state.count - 1 })),
  reset:     () => set({ count: 0 }),
  setUser:   (user) => set({ user }),

  // Computed / Actions using get()
  doubleCount: () => get().count * 2,
}));

// Component usage — no Provider needed!
function Counter() {
  const { count, increment, decrement } = useStore();

  return (
    <div>
      <p>{count}</p>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </div>
  );
}

// Select only what you need (performance)
const count = useStore(state => state.count); // Only re-renders on count change
```

---

## 29. Performance Optimization

### React.memo — Prevent Unnecessary Re-renders

```jsx
// Wrapping a component with React.memo
// Only re-renders if props actually changed
const ExpensiveComponent = React.memo(({ data, onUpdate }) => {
  console.log("Rendering...");
  return <div>{data.name}</div>;
});

// Custom comparison function
const Component = React.memo(
  ({ user }) => <div>{user.name}</div>,
  (prevProps, nextProps) => prevProps.user.id === nextProps.user.id
  // Return true = skip re-render (props are equal)
  // Return false = re-render (props changed)
);
```

### Code Splitting & Lazy Loading

```jsx
import { lazy, Suspense } from "react";

// Lazy load component (creates separate bundle chunk)
const Dashboard   = lazy(() => import("./pages/Dashboard"));
const UserProfile = lazy(() => import("./pages/UserProfile"));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/dashboard"    element={<Dashboard />} />
        <Route path="/profile/:id"  element={<UserProfile />} />
      </Routes>
    </Suspense>
  );
}
```

### Virtualization — Large Lists

```jsx
// npm install react-window
import { FixedSizeList } from "react-window";

// Only renders visible items — handles 100,000+ items smoothly!
function VirtualList({ items }) {
  const Row = ({ index, style }) => (
    <div style={style}> {/* style is required for positioning */}
      {items[index].name}
    </div>
  );

  return (
    <FixedSizeList
      height={600}        // Container height
      itemCount={items.length}
      itemSize={50}       // Each row height
      width="100%"
    >
      {Row}
    </FixedSizeList>
  );
}
```

### Performance Checklist

```
✅ Use React.memo for expensive components
✅ Use useCallback for functions passed as props
✅ Use useMemo for expensive calculations
✅ Use lazy() + Suspense for code splitting
✅ Virtualize long lists (react-window)
✅ Avoid creating objects/arrays in render (use useMemo)
✅ Use production build (React DevTools shows)
✅ Batch state updates (automatic in React 18)
✅ useTransition for non-urgent updates
✅ Avoid prop drilling deep — use Context or state manager
✅ Profile with React DevTools Profiler
```

---

## 30. Forms in React

### Controlled Components (Preferred)

```jsx
// React state is the "single source of truth" for input values
function LoginForm() {
  const [formData, setFormData] = useState({
    email: "",
    password: "",
    remember: false,
  });
  const [errors, setErrors] = useState({});
  const [loading, setLoading] = useState(false);

  const handleChange = (e) => {
    const { name, value, type, checked } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: type === "checkbox" ? checked : value
    }));
    // Clear error on change
    if (errors[name]) setErrors(prev => ({ ...prev, [name]: "" }));
  };

  const validate = () => {
    const newErrors = {};
    if (!formData.email) newErrors.email = "Email is required";
    else if (!/\S+@\S+\.\S+/.test(formData.email)) newErrors.email = "Invalid email";
    if (!formData.password) newErrors.password = "Password is required";
    else if (formData.password.length < 8) newErrors.password = "Min 8 characters";
    return newErrors;
  };

  const handleSubmit = async (e) => {
    e.preventDefault(); // Prevent page reload!

    const newErrors = validate();
    if (Object.keys(newErrors).length > 0) {
      setErrors(newErrors);
      return;
    }

    setLoading(true);
    try {
      await loginAPI(formData);
    } catch (err) {
      setErrors({ submit: err.message });
    } finally {
      setLoading(false);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <input
          type="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
          placeholder="Email"
          aria-describedby="email-error"
        />
        {errors.email && <span id="email-error" role="alert">{errors.email}</span>}
      </div>

      <div>
        <input
          type="password"
          name="password"
          value={formData.password}
          onChange={handleChange}
          placeholder="Password"
        />
        {errors.password && <span>{errors.password}</span>}
      </div>

      <label>
        <input
          type="checkbox"
          name="remember"
          checked={formData.remember}
          onChange={handleChange}
        />
        Remember me
      </label>

      {errors.submit && <div className="error">{errors.submit}</div>}

      <button type="submit" disabled={loading}>
        {loading ? "Logging in..." : "Login"}
      </button>
    </form>
  );
}
```

### React Hook Form (Most Popular Form Library)

```jsx
// npm install react-hook-form
import { useForm, Controller } from "react-hook-form";

function SignupForm() {
  const {
    register,
    handleSubmit,
    watch,
    formState: { errors, isSubmitting },
    reset,
    control,
  } = useForm({
    defaultValues: { name: "", email: "", password: "", confirmPassword: "" }
  });

  const password = watch("password");

  const onSubmit = async (data) => {
    await signupAPI(data);
    reset();
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input
        {...register("name", {
          required: "Name is required",
          minLength: { value: 2, message: "Min 2 characters" }
        })}
        placeholder="Name"
      />
      {errors.name && <span>{errors.name.message}</span>}

      <input
        {...register("email", {
          required: "Email required",
          pattern: { value: /\S+@\S+\.\S+/, message: "Invalid email" }
        })}
        placeholder="Email"
      />
      {errors.email && <span>{errors.email.message}</span>}

      <input
        type="password"
        {...register("password", {
          required: "Password required",
          minLength: { value: 8, message: "Min 8 chars" },
          pattern: {
            value: /(?=.*[A-Z])(?=.*[0-9])/,
            message: "Must contain uppercase and number"
          }
        })}
      />
      {errors.password && <span>{errors.password.message}</span>}

      <input
        type="password"
        {...register("confirmPassword", {
          validate: value => value === password || "Passwords don't match"
        })}
      />
      {errors.confirmPassword && <span>{errors.confirmPassword.message}</span>}

      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? "Signing up..." : "Sign Up"}
      </button>
    </form>
  );
}
```

---

## 31. Custom Hooks

Custom hooks let you **extract and reuse stateful logic** between components.

```jsx
// Rule: Custom hook names MUST start with "use"

// 1. useFetch — generic data fetching
function useFetch(url) {
  const [data, setData]       = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError]     = useState(null);

  useEffect(() => {
    let cancelled = false;

    const fetchData = async () => {
      try {
        setLoading(true);
        setError(null);
        const res = await fetch(url);
        if (!res.ok) throw new Error(`HTTP ${res.status}`);
        const json = await res.json();
        if (!cancelled) setData(json);
      } catch (err) {
        if (!cancelled) setError(err.message);
      } finally {
        if (!cancelled) setLoading(false);
      }
    };

    fetchData();
    return () => { cancelled = true; };
  }, [url]);

  return { data, loading, error };
}

// Usage
function UserProfile({ id }) {
  const { data: user, loading, error } = useFetch(`/api/users/${id}`);
  if (loading) return <Spinner />;
  if (error)   return <Error msg={error} />;
  return <div>{user.name}</div>;
}

// 2. useLocalStorage
function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch {
      return initialValue;
    }
  });

  const setStoredValue = useCallback((newValue) => {
    setValue(newValue);
    try {
      window.localStorage.setItem(key, JSON.stringify(newValue));
    } catch (err) {
      console.error("localStorage error:", err);
    }
  }, [key]);

  return [value, setStoredValue];
}

// 3. useDebounce — delay value update
function useDebounce(value, delay = 300) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => setDebouncedValue(value), delay);
    return () => clearTimeout(timer);
  }, [value, delay]);

  return debouncedValue;
}

// Usage: Search input
function SearchBox() {
  const [query, setQuery] = useState("");
  const debouncedQuery = useDebounce(query, 500);

  useEffect(() => {
    if (debouncedQuery) {
      searchAPI(debouncedQuery); // Only fires 500ms after user stops typing
    }
  }, [debouncedQuery]);

  return <input value={query} onChange={e => setQuery(e.target.value)} />;
}

// 4. useToggle
function useToggle(initialValue = false) {
  const [value, setValue] = useState(initialValue);
  const toggle = useCallback(() => setValue(v => !v), []);
  const setTrue  = useCallback(() => setValue(true), []);
  const setFalse = useCallback(() => setValue(false), []);
  return [value, toggle, setTrue, setFalse];
}

// 5. useClickOutside — close dropdown on outside click
function useClickOutside(ref, callback) {
  useEffect(() => {
    function handleClick(e) {
      if (ref.current && !ref.current.contains(e.target)) {
        callback();
      }
    }
    document.addEventListener("mousedown", handleClick);
    return () => document.removeEventListener("mousedown", handleClick);
  }, [ref, callback]);
}

// 6. useWindowSize
function useWindowSize() {
  const [size, setSize] = useState({
    width: window.innerWidth,
    height: window.innerHeight,
  });

  useEffect(() => {
    const handleResize = () => setSize({
      width: window.innerWidth,
      height: window.innerHeight,
    });
    window.addEventListener("resize", handleResize);
    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return size;
}
```

---

## 32. React Patterns

### Compound Components

```jsx
// Components that work together and share state implicitly
// Example: <Select> pattern

const SelectContext = createContext(null);

function Select({ children, value, onChange }) {
  return (
    <SelectContext.Provider value={{ selectedValue: value, onChange }}>
      <div className="select-container">{children}</div>
    </SelectContext.Provider>
  );
}

function Option({ value, children }) {
  const { selectedValue, onChange } = useContext(SelectContext);
  const isSelected = selectedValue === value;

  return (
    <div
      className={`option ${isSelected ? "selected" : ""}`}
      onClick={() => onChange(value)}
    >
      {children}
    </div>
  );
}

Select.Option = Option; // Attach as static property

// Usage
<Select value={selected} onChange={setSelected}>
  <Select.Option value="react">React</Select.Option>
  <Select.Option value="vue">Vue</Select.Option>
  <Select.Option value="angular">Angular</Select.Option>
</Select>
```

### Render Props Pattern

```jsx
// Pass a function as prop that returns JSX
function MouseTracker({ render }) {
  const [pos, setPos] = useState({ x: 0, y: 0 });

  return (
    <div onMouseMove={e => setPos({ x: e.clientX, y: e.clientY })}>
      {render(pos)} {/* Call the render function with data */}
    </div>
  );
}

// Usage
<MouseTracker render={({ x, y }) => (
  <p>Mouse is at ({x}, {y})</p>
)} />

// Modern approach: use custom hook instead (usually cleaner)
function useMouse() {
  const [pos, setPos] = useState({ x: 0, y: 0 });
  useEffect(() => {
    const handler = e => setPos({ x: e.clientX, y: e.clientY });
    window.addEventListener("mousemove", handler);
    return () => window.removeEventListener("mousemove", handler);
  }, []);
  return pos;
}
```

### Higher-Order Components (HOC)

```jsx
// A function that takes a component and returns an enhanced component
function withAuth(WrappedComponent) {
  return function AuthenticatedComponent(props) {
    const { isLoggedIn } = useAuth();

    if (!isLoggedIn) {
      return <Navigate to="/login" />;
    }

    return <WrappedComponent {...props} />;
  };
}

// Usage
const ProtectedDashboard = withAuth(Dashboard);

// withLoading HOC
function withLoading(WrappedComponent) {
  return function ({ loading, ...props }) {
    if (loading) return <Spinner />;
    return <WrappedComponent {...props} />;
  };
}
```

---

## 33. Testing in React

### Jest + React Testing Library

```jsx
// npm install --save-dev @testing-library/react @testing-library/jest-dom

import { render, screen, fireEvent, waitFor } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import { Counter } from "./Counter";

describe("Counter Component", () => {
  // Test basic rendering
  test("renders initial count of 0", () => {
    render(<Counter />);
    expect(screen.getByText("Count: 0")).toBeInTheDocument();
  });

  // Test user interaction
  test("increments count when button is clicked", async () => {
    const user = userEvent.setup();
    render(<Counter />);

    const button = screen.getByRole("button", { name: /increment/i });
    await user.click(button);

    expect(screen.getByText("Count: 1")).toBeInTheDocument();
  });

  // Test async behavior
  test("loads and displays users", async () => {
    // Mock fetch
    global.fetch = jest.fn().mockResolvedValue({
      ok: true,
      json: async () => [{ id: 1, name: "Alice" }]
    });

    render(<UserList />);

    expect(screen.getByText("Loading...")).toBeInTheDocument();

    await waitFor(() => {
      expect(screen.getByText("Alice")).toBeInTheDocument();
    });
  });

  // Test with context
  test("shows user name when logged in", () => {
    const mockUser = { name: "Bob" };
    render(
      <AuthContext.Provider value={{ user: mockUser, isLoggedIn: true }}>
        <NavBar />
      </AuthContext.Provider>
    );
    expect(screen.getByText("Hello, Bob!")).toBeInTheDocument();
  });
});

// Testing Library Queries (priority order):
// getByRole           → Best: uses ARIA roles (button, textbox, heading)
// getByLabelText      → Form elements with labels
// getByPlaceholderText → Input placeholder
// getByText           → Visible text content
// getByDisplayValue   → Current value of form element
// getByAltText        → Image alt text
// getByTitle          → Title attribute
// getByTestId         → data-testid attribute (last resort)

// get* → throws if not found
// query* → returns null if not found (for asserting absence)
// find* → async, returns promise (waits for element)
```

---

## 34. Interview Q&A — JS

### Core Questions

**Q1: What is the difference between `null` and `undefined`?**
> `undefined` means a variable was declared but never assigned a value. `null` is an intentional "no value" — a developer explicitly sets it. `typeof null === "object"` (historic bug). `typeof undefined === "undefined"`. Use `null` to indicate "empty on purpose."

**Q2: Explain `this` in JavaScript.**
> `this` refers to the object that called the function. In a method: the object. In a regular function: `window` (or `undefined` in strict mode). Arrow functions: no own `this`, inherit from enclosing scope. Can be explicitly set with `call()`, `apply()`, `bind()`.

**Q3: What is event delegation?**
> Instead of attaching event listeners to each child element, attach ONE listener to the parent. Use `event.target` to determine which child was clicked. Benefits: memory efficient, handles dynamically added elements.

**Q4: What is debouncing vs throttling?**
> **Debouncing:** Delays function execution until after a wait period since last call. Use for search inputs (only search after typing stops). **Throttling:** Limits function execution to once per time period. Use for scroll/resize events.

**Q5: What is the difference between `==` and `===`?**
> `==` performs type coercion before comparison (`"5" == 5` → true). `===` is strict — no coercion, checks type AND value (`"5" === 5` → false). Always use `===` to avoid surprising coercion bugs.

**Q6: Explain Promises and async/await.**
> A Promise represents a value that may be available now, later, or never. It has three states: pending, fulfilled, rejected. `async/await` is syntactic sugar over Promises that makes async code look synchronous. `await` pauses execution until the Promise settles. Error handling: try/catch with async/await.

**Q7: What is the Event Loop?**
> JS is single-threaded. The Event Loop manages async execution: synchronous code runs on the Call Stack. Async tasks (setTimeout, fetch) go to Web APIs. When done, callbacks go to Macro-task Queue (setTimeout) or Micro-task Queue (Promises). Event Loop: empty Call Stack → drain Microtask Queue completely → process one Macro-task → repeat.

**Q8: Difference between `call`, `apply`, and `bind`?**
> All explicitly set `this`. `call(ctx, arg1, arg2)` — calls immediately, args listed. `apply(ctx, [arg1, arg2])` — calls immediately, args as array. `bind(ctx, arg1)` — returns a NEW function with `this` bound, doesn't call immediately.

**Q9: What is a generator function?**
> A function that can pause execution (`yield`) and resume. Returns an iterator. Useful for: infinite sequences, lazy evaluation, custom iteration, async flows. `function*` syntax with `yield` keyword.

**Q10: Shallow copy vs Deep copy?**
```javascript
// Shallow — top-level values are copied, nested objects are still references
const shallow = { ...original };          // spread
const shallow2 = Object.assign({}, original);

// Deep — completely independent copy
const deep = JSON.parse(JSON.stringify(original)); // Works for plain objects
const deep2 = structuredClone(original); // Modern (ES2022) — handles more types
```

---

## 35. Interview Q&A — React

**Q1: What is the Virtual DOM and how does it work?**
> Virtual DOM is a lightweight JavaScript representation of the real DOM. When state changes, React creates a new Virtual DOM tree, diffs it against the previous one (reconciliation), and only updates the parts that actually changed in the real DOM. This is more efficient than re-rendering the entire DOM.

**Q2: What are React Hooks and why were they introduced?**
> Hooks (introduced in React 16.8) let functional components use state, lifecycle, and other React features that were previously only available in class components. They allow better logic reuse (custom hooks), reduce boilerplate, and make code more readable.

**Q3: What is the difference between `useMemo` and `useCallback`?**
> `useMemo` memoizes the **result** of a computation — use for expensive calculated values. `useCallback` memoizes the **function itself** — use when passing functions as props to prevent child re-renders (with React.memo).

**Q4: Explain the rules of Hooks.**
> 1. Only call hooks at the TOP LEVEL — not inside loops, conditions, or nested functions. 2. Only call hooks from REACT FUNCTIONS — functional components or custom hooks. Not regular JS functions.

**Q5: What is React.memo?**
> A higher-order component that memoizes a functional component. It only re-renders if props change. Use with `useCallback` for function props. Similar to `PureComponent` for class components.

**Q6: What is the difference between state and props?**
> **Props** — Passed from parent to child, read-only in the child. **State** — Managed within the component, can be changed (triggers re-render). Props are like function arguments; state is like local variables.

**Q7: What is prop drilling and how do you solve it?**
> Prop drilling is passing props through many intermediate components that don't need the data. Solutions: Context API (for global data like auth, theme), Redux/Zustand (complex state), component composition.

**Q8: What is reconciliation in React?**
> Reconciliation is how React updates the DOM. When state/props change, React re-renders the component tree, creates a new Virtual DOM, and uses the "diffing algorithm" to find minimal changes needed. The `key` prop helps React identify elements efficiently.

**Q9: When to use `useReducer` over `useState`?**
> Use `useReducer` when: state has complex logic or multiple sub-values, next state depends on previous, state updates are complex objects, you want Redux-like patterns locally.

**Q10: What is Strict Mode in React?**
> `<React.StrictMode>` is a development tool that: activates additional warnings, detects deprecated APIs, runs effects twice (to catch side effects in effects), helps identify problems before they cause bugs.

---

## 36. Coding Problems Cheatsheet

### JavaScript Challenges

```javascript
// 1. Flatten nested array
const flatten = (arr) => arr.flat(Infinity);
// or:
const flatten2 = (arr) => arr.reduce(
  (flat, item) => flat.concat(Array.isArray(item) ? flatten2(item) : item), []
);

// 2. Deep clone object
const deepClone = obj => structuredClone(obj); // Modern
const deepClone2 = obj => JSON.parse(JSON.stringify(obj)); // Simple

// 3. Debounce function
function debounce(fn, delay) {
  let timer;
  return function(...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

// 4. Throttle function
function throttle(fn, limit) {
  let lastCall = 0;
  return function(...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      return fn.apply(this, args);
    }
  };
}

// 5. Memoize function
function memoize(fn) {
  const cache = new Map();
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}

// 6. Curry function
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    }
    return function(...moreArgs) {
      return curried.apply(this, args.concat(moreArgs));
    };
  };
}
const add = curry((a, b, c) => a + b + c);
add(1)(2)(3);   // 6
add(1, 2)(3);   // 6
add(1)(2, 3);   // 6

// 7. Pipe / Compose
const pipe = (...fns) => x => fns.reduce((v, fn) => fn(v), x);
const compose = (...fns) => x => fns.reduceRight((v, fn) => fn(v), x);

const double = x => x * 2;
const addOne = x => x + 1;
const square = x => x * x;

pipe(double, addOne, square)(3); // ((3*2)+1)^2 = 49
compose(square, addOne, double)(3); // Same operations, different order

// 8. Promise.all implementation
function promiseAll(promises) {
  return new Promise((resolve, reject) => {
    const results = [];
    let completed = 0;

    promises.forEach((promise, i) => {
      Promise.resolve(promise).then(value => {
        results[i] = value;
        if (++completed === promises.length) resolve(results);
      }).catch(reject);
    });
  });
}

// 9. Group array by property
const groupBy = (arr, key) => arr.reduce((groups, item) => {
  const group = item[key];
  groups[group] = groups[group] ?? [];
  groups[group].push(item);
  return groups;
}, {});

// 10. Deep equality check
function deepEqual(a, b) {
  if (a === b) return true;
  if (typeof a !== typeof b) return false;
  if (typeof a !== "object" || a === null) return false;
  const keysA = Object.keys(a), keysB = Object.keys(b);
  if (keysA.length !== keysB.length) return false;
  return keysA.every(key => deepEqual(a[key], b[key]));
}

// 11. Event Emitter class
class EventEmitter {
  constructor() { this.events = {}; }
  on(event, listener) {
    (this.events[event] ??= []).push(listener);
    return this;
  }
  off(event, listener) {
    this.events[event] = (this.events[event] || []).filter(l => l !== listener);
    return this;
  }
  emit(event, ...args) {
    (this.events[event] || []).forEach(l => l(...args));
    return this;
  }
  once(event, listener) {
    const wrapper = (...args) => { listener(...args); this.off(event, wrapper); };
    return this.on(event, wrapper);
  }
}

// 12. Implement Array.prototype.reduce from scratch
Array.prototype.myReduce = function(callback, initialValue) {
  let acc = initialValue !== undefined ? initialValue : this[0];
  let start = initialValue !== undefined ? 0 : 1;
  for (let i = start; i < this.length; i++) {
    acc = callback(acc, this[i], i, this);
  }
  return acc;
};
```

### React Coding Patterns

```jsx
// 1. Infinite Scroll
function useInfiniteScroll(fetchMore) {
  const [page, setPage] = useState(1);
  const loaderRef = useRef(null);

  useEffect(() => {
    const observer = new IntersectionObserver(entries => {
      if (entries[0].isIntersecting) {
        setPage(p => p + 1);
        fetchMore(page + 1);
      }
    });
    if (loaderRef.current) observer.observe(loaderRef.current);
    return () => observer.disconnect();
  }, []);

  return loaderRef;
}

// 2. Pagination Component
function Pagination({ total, page, perPage, onChange }) {
  const totalPages = Math.ceil(total / perPage);

  return (
    <div>
      <button onClick={() => onChange(page - 1)} disabled={page === 1}>←</button>
      {Array.from({ length: totalPages }, (_, i) => i + 1).map(p => (
        <button
          key={p}
          onClick={() => onChange(p)}
          className={p === page ? "active" : ""}
        >
          {p}
        </button>
      ))}
      <button onClick={() => onChange(page + 1)} disabled={page === totalPages}>→</button>
    </div>
  );
}

// 3. Accordion Component
function Accordion({ items }) {
  const [openIndex, setOpenIndex] = useState(null);

  return (
    <div>
      {items.map((item, i) => (
        <div key={i}>
          <button onClick={() => setOpenIndex(openIndex === i ? null : i)}>
            {item.title}
          </button>
          {openIndex === i && <div>{item.content}</div>}
        </div>
      ))}
    </div>
  );
}

// 4. Star Rating Component
function StarRating({ max = 5, value = 0, onChange }) {
  const [hover, setHover] = useState(0);

  return (
    <div>
      {Array.from({ length: max }, (_, i) => i + 1).map(star => (
        <span
          key={star}
          style={{ color: star <= (hover || value) ? "gold" : "gray", cursor: "pointer" }}
          onMouseEnter={() => setHover(star)}
          onMouseLeave={() => setHover(0)}
          onClick={() => onChange(star)}
        >
          ★
        </span>
      ))}
    </div>
  );
}
```

---

## 🏆 Quick Revision Summary

```
JAVASCRIPT CORE
├── Variables: const (default) > let > var (avoid)
├── Types: 7 primitives + Reference types
├── Coercion: == (loose) vs === (strict)
├── Functions: Declaration, Expression, Arrow
├── Scope: Global > Function > Block (let/const)
├── Closures: Inner function remembers outer scope
├── Hoisting: var (undefined), let/const (TDZ), function (fully)
├── Async: Callbacks → Promises → async/await
├── Event Loop: Sync → Microtasks → Macrotasks
└── ES6+: Destructuring, Spread/Rest, Template literals, Modules

ARRAYS: map, filter, reduce, find, some, every, flat, flatMap
OBJECTS: spread, Object.keys/values/entries, optional chaining ?., ??

REACT CORE
├── JSX — HTML-like syntax, compiles to createElement
├── Components — Functional (preferred) or Class
├── Props — Read-only, parent → child
├── State — useState, triggers re-render
├── Effects — useEffect (side effects, data fetching)
└── Rules of Hooks — Top level only, React functions only

KEY HOOKS
├── useState   — Local state
├── useEffect  — Side effects
├── useContext — Consume context
├── useReducer — Complex state
├── useRef     — DOM refs / persistent values
├── useMemo    — Memoize values
└── useCallback — Memoize functions

PERFORMANCE
├── React.memo — Skip re-renders if props unchanged
├── useMemo    — Cache expensive computations
├── useCallback — Stable function references
├── lazy()     — Code splitting
└── Virtualize — Long lists

INTERVIEW KEY TOPICS
├── Virtual DOM & Reconciliation
├── Closure & var-in-loop trap
├── Event Loop execution order
├── this binding (call/apply/bind)
├── Promises vs async/await
├── useState vs useReducer
├── useEffect dependency array
└── React key prop importance
```

---

> 📌 **Pro Interview Tips:**
> 1. **Always explain your thinking** — interviewers care about your process
> 2. **Mention trade-offs** — "I'd use Context for small apps, Redux for large ones because..."
> 3. **Security awareness** — XSS with `innerHTML`, sanitize inputs
> 4. **Accessibility** — Use semantic HTML, ARIA labels, keyboard navigation
> 5. **Performance** — React.memo, useMemo, lazy loading are huge plus points
> 6. **TypeScript** — Mention you know or are learning it; highly valued
> 7. **Testing** — Even basic knowledge of Jest/RTL stands out

---

**⭐ Star this repo if these notes helped you crack your interview!**
