# JavaScript – Functions

---

## 📘 What is a Function?

A function is a **reusable block of code** that performs a specific task. Functions are first-class citizens in JS — they can be stored in variables, passed as arguments, and returned from other functions.

---

## 🗂️ Ways to Define Functions

### Function Declaration
```js
function greet(name) {
  return "Hello, " + name;
}

greet("Ali");  // "Hello, Ali"
```
> Hoisted — can be called before it's defined in the code.

### Function Expression
```js
const greet = function(name) {
  return "Hello, " + name;
};
```
> Not hoisted — must be defined before calling.

### Arrow Function (ES6)
```js
const greet = (name) => "Hello, " + name;

// With body (needs explicit return)
const add = (a, b) => {
  const sum = a + b;
  return sum;
};

// Single param — no parentheses needed
const double = n => n * 2;

// No params
const sayHi = () => "Hi!";
```

### Constructor Function (older style)
```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}
const user = new Person("Ali", 25);
```

---

## 🔧 Function Parameters

### Default Parameters
```js
function greet(name = "Guest") {
  return "Hello, " + name;
}
greet();        // "Hello, Guest"
greet("Ali");   // "Hello, Ali"
```

### Rest Parameters (`...`)
```js
function sum(...numbers) {
  return numbers.reduce((total, n) => total + n, 0);
}
sum(1, 2, 3, 4);  // 10
```

### Arguments Object (only in regular functions, NOT arrow)
```js
function showArgs() {
  console.log(arguments);  // array-like object
}
showArgs(1, 2, 3);  // Arguments [1, 2, 3]
```

---

## 🔄 Return Values

```js
function add(a, b) {
  return a + b;  // exits function and returns value
}

// Functions without return → return undefined
function doNothing() {}
doNothing();  // undefined
```

---

## 🧠 Scope

```js
let global = "I am global";

function outer() {
  let outerVar = "outer";

  function inner() {
    let innerVar = "inner";
    console.log(global);   // ✅ accessible
    console.log(outerVar); // ✅ accessible (closure)
    console.log(innerVar); // ✅ accessible
  }

  inner();
  console.log(innerVar);  // ❌ ReferenceError
}
```

---

## 🔒 Closures

A closure is when an inner function **remembers variables from its outer scope** even after the outer function has finished.

```js
function counter() {
  let count = 0;             // lives in outer scope
  return function() {
    count++;
    return count;
  };
}

const increment = counter();
increment();  // 1
increment();  // 2
increment();  // 3
// count is preserved in the closure
```

```js
// Practical: create private state
function makeMultiplier(factor) {
  return (num) => num * factor;
}

const double = makeMultiplier(2);
const triple = makeMultiplier(3);
double(5);  // 10
triple(5);  // 15
```

---

## 🏹 Arrow Functions vs Regular Functions

| Feature | Regular Function | Arrow Function |
|---------|-----------------|----------------|
| `this` binding | Dynamic (own `this`) | Lexical (inherits `this`) |
| `arguments` object | ✅ Yes | ❌ No |
| Use as constructor | ✅ Yes | ❌ No |
| Hoisted | Declaration: ✅ | ❌ No |
| Best for | Methods, constructors | Callbacks, short functions |

```js
const obj = {
  name: "Ali",
  greetRegular: function() {
    console.log(this.name);  // "Ali" ✅
  },
  greetArrow: () => {
    console.log(this.name);  // undefined ❌ (this = outer scope)
  }
};
```

---

## ⬆️ Hoisting

```js
// Function Declaration — hoisted fully
sayHi();           // ✅ works
function sayHi() { console.log("Hi"); }

// Function Expression — NOT hoisted
greet();           // ❌ TypeError
const greet = function() { console.log("Hello"); };
```

---

## 📝 Interview Questions

**Q1. What is the difference between a function declaration and a function expression?**
> A declaration (`function name() {}`) is hoisted — it can be called before it appears in code. An expression (`const fn = function() {}`) is not hoisted and must be defined before calling.

**Q2. What is a closure?**
> A closure is a function that retains access to variables from its outer (enclosing) scope even after that outer function has returned. It allows data to be "remembered" privately — commonly used for counter functions, factories, and module patterns.

**Q3. What is the key difference between arrow functions and regular functions?**
> The main difference is how `this` is handled. Regular functions have their own `this` based on how they're called. Arrow functions don't have their own `this` — they inherit it from the surrounding lexical scope. Arrow functions also have no `arguments` object and cannot be used as constructors.

**Q4. What are default parameters?**
> Default parameters let you specify a fallback value if no argument (or `undefined`) is passed: `function greet(name = "Guest")`. This replaces the old `name = name || "Guest"` pattern.

**Q5. What is the difference between `arguments` and rest parameters `...`?**
> `arguments` is an array-like object available in regular functions. Rest parameters (`...args`) collect all extra arguments into a real array and work in arrow functions too. Rest parameters are preferred in modern JS.

**Q6. What does a function return if there is no `return` statement?**
> It returns `undefined` by default.

**Q7. What is a Higher-Order Function?**
> A function that takes another function as an argument or returns a function. Examples: `map`, `filter`, `forEach`, `reduce`. They are enabled by JavaScript treating functions as first-class citizens.

---

*Next: Arrays →*