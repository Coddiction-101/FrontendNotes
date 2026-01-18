# JavaScript — Part 3 (Advanced Concepts & Real-World Patterns)

> *From understanding how JavaScript works internally to building production-grade async features.*

---

## Table of Contents

1. Introduction
2. Scope, Execution Context & Closures
3. Encapsulation & Real-World Closure Use Cases
4. `this` Keyword — Deep Dive
5. Object-Oriented JavaScript
6. Prototypal vs Classical Inheritance
7. Asynchronous JavaScript
8. Promises & Async/Await
9. Fetch API & HTTP Fundamentals
10. Real-World Project: Dynamic User Cards
11. Key Takeaways
12. What to Learn Next

---

## 1. Introduction

JavaScript is the backbone of modern web development. As applications grow complex, understanding **how JavaScript actually works** becomes more important than just writing syntax.

This guide focuses on:

* Internal mechanics (scope, execution context)
* Real-world design patterns
* Asynchronous programming
* Practical project-level thinking

If you understand this file well, **React, Node.js, and system design concepts become much easier**.

---

## 2. The Foundation: Scope, Execution Context & Closures

### 2.1 Scope in JavaScript

Scope defines **where a variable can be accessed**.

#### Types of Scope

* **Global Scope**
  Accessible everywhere.

* **Function Scope (`var`)**
  Accessible only inside the function.

* **Block Scope (`let`, `const`)**
  Accessible only inside `{}` blocks.

```js
if (true) {
  let x = 10;
}
// x ❌ not accessible here
```

✅ Prefer `let` and `const` for predictable behavior.

---

### 2.2 Execution Context (Behind the Scenes)

Every time JavaScript runs code, it creates an **Execution Context**.

#### Two Phases

1. **Memory Creation Phase**

   * Variables → `undefined`
   * Functions → stored completely

2. **Execution Phase**

   * Code runs line by line
   * Variables get actual values

📌 Understanding this explains:

* Hoisting
* Call stack
* Unexpected `undefined`

---

### 2.3 Lexical Scoping

JavaScript uses **lexical scoping**, meaning:

> Scope is decided by **where code is written**, not how it is called.

```js
function outer() {
  let a = 12;
  function inner() {
    console.log(a); // 12
  }
  inner();
}
outer();
```

---

### 2.4 Closures — Memory That Persists

A **closure** is formed when a function remembers variables from its outer scope even after that outer function finishes execution.

#### Example: Private Counter

```js
function createCounter() {
  let count = 0;
  return function () {
    count++;
    console.log(count);
  };
}

const counter = createCounter();
counter(); // 1
counter(); // 2
```

📌 Closures enable:

* Data privacy
* State management
* Encapsulation

---

## 3. Encapsulation Using Closures

### Click Limiter Example

```js
function clickLimiter() {
  let clicks = 0;
  return function () {
    if (clicks < 5) {
      clicks++;
      console.log(`Clicked ${clicks} times`);
    } else {
      console.log('Limit exceeded');
    }
  };
}
```

✅ `clicks` is **private**
✅ Logic is protected from external access

---

## 4. Real-World Component: Toaster Notification

### Concept

* Parent function → configuration
* Child function → execution
* Closure → preserves config

```js
function createToaster(config) {
  return function (message) {
    // Create toast
    // Apply config styles
    // Auto remove after duration
  };
}

const toaster = createToaster({
  position: 'top-right',
  theme: 'dark',
  duration: 3000
});

toaster('File uploaded successfully');
```

📌 Used heavily in:

* Notifications
* Alerts
* UI feedback systems

---

## 5. `this` Keyword — Context Matters

### How `this` is Determined

| Scenario       | Value of `this`       |
| -------------- | --------------------- |
| Global         | `window`              |
| Function       | `window` (non-strict) |
| Object Method  | Object itself         |
| Event Listener | Target element        |
| Class          | Instance              |

---

### Arrow Functions & `this`

Arrow functions **do not have their own `this`**.

```js
const obj = {
  name: 'Harsh',
  normal() {
    return this.name;
  },
  arrow: () => {
    return this.name;
  }
};
```

✔ Use **normal functions** for object methods.

---

### Manual Binding

```js
func.call(obj, a, b);
func.apply(obj, [a, b]);
const bound = func.bind(obj);
```

* `call` → immediate
* `apply` → immediate (array)
* `bind` → returns new function

---

## 6. Object-Oriented JavaScript

### Constructor Function

```js
function Pencil(name, price) {
  this.name = name;
  this.price = price;
}
```

---

### Prototypes (Memory Efficient)

```js
Pencil.prototype.write = function () {
  console.log(`${this.name} is writing`);
};
```

✔ Shared across all instances

---

### ES6 Classes (Cleaner Syntax)

```js
class Pencil {
  constructor(name, price) {
    this.name = name;
    this.price = price;
  }
  write() {
    console.log(`${this.name} writes`);
  }
}
```

---

### Inheritance

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

class Admin extends User {
  constructor(name) {
    super(name);
    this.role = 'admin';
  }
}
```

---

## 7. Prototypal vs Classical Inheritance

### Prototypal

```js
const coffee = {
  drink() {
    console.log('Good');
  }
};

const arabica = Object.create(coffee);
arabica.taste = 'bitter';
```

📌 JavaScript is **prototype-based by nature**.

---

## 8. Asynchronous JavaScript

### Sync vs Async

```js
console.log('A');
setTimeout(() => console.log('B'), 2000);
console.log('C');
```

Output:

```
A
C
B
```

---

### Callback Hell (Problem)

```js
getUser(() => {
  getPosts(() => {
    getComments(() => {});
  });
});
```

❌ Hard to read
❌ Hard to debug

---

## 9. Promises & Async/Await

### Promise

```js
const promise = new Promise((resolve, reject) => {
  resolve('Success');
});
```

### Async / Await

```js
async function fetchData() {
  try {
    const data = await promise;
    console.log(data);
  } catch (err) {
    console.log(err);
  }
}
```

✔ Cleaner
✔ Readable
✔ Debug-friendly

---

## 10. Fetch API & HTTP Basics

### GET Request

```js
fetch(url)
  .then(res => res.json())
  .then(data => console.log(data));
```

### POST Request

```js
fetch(url, {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify(data)
});
```

---

## 11. Real-World Project: Dynamic User Cards

### Flow

1. Fetch users
2. Parse JSON
3. Clear container
4. Render cards
5. Refresh on button click

```js
function getUsers() {
  fetch('https://randomuser.me/api/?results=3')
    .then(res => res.json())
    .then(data => {
      users.innerHTML = '';
      data.results.forEach(user => {
        // create card
      });
    });
}
```

📌 Covers:

* API
* Async JS
* DOM
* UI updates

---

## 12. Key Takeaways

* JavaScript is **event-driven & async**
* Closures = power
* `this` depends on **call site**
* Prototypes save memory
* Async/Await is mandatory skill

---

## 13. What to Learn Next

* JavaScript Event Loop (microtasks vs macrotasks)
* Debouncing & throttling
* Design patterns
* React fundamentals
* Node.js + Express

---

### Final Thought

> You don’t become good at JavaScript by watching.
> You become good by **building, breaking, and fixing**.

Keep coding. Keep questioning. Keep leveling up. 🚀

