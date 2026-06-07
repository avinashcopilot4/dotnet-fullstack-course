# JavaScript – Introduction, Variables & Data Types

---

## 📘 What is JavaScript?

JavaScript is a **lightweight, interpreted, dynamically-typed** programming language. It runs in the browser (client-side) and on the server (Node.js). It is the language that makes web pages **interactive**.

---

## 📦 Variables

### Three ways to declare variables

```js
var name = "Alice";    // old way — avoid in modern JS
let age = 25;          // block-scoped — prefer for changing values
const PI = 3.14;       // block-scoped — cannot be reassigned
```

### `var` vs `let` vs `const`

| Feature | `var` | `let` | `const` |
|---------|-------|-------|---------|
| Scope | Function | Block | Block |
| Hoisting | ✅ (undefined) | ✅ (TDZ error) | ✅ (TDZ error) |
| Re-declare | ✅ | ❌ | ❌ |
| Re-assign | ✅ | ✅ | ❌ |

```js
// Block scope example
{
  let x = 10;
  const y = 20;
  var z = 30;
}
console.log(z); // 30 — var leaks out of block
console.log(x); // ReferenceError — let is block-scoped
```

---

## 🗂️ Data Types

### Primitive Types (7 total)

```js
let name    = "Alice";        // String
let age     = 25;             // Number
let big     = 9007199254740993n; // BigInt
let isAdmin = true;           // Boolean
let score   = null;           // Null (intentional empty)
let address;                  // Undefined (declared, not assigned)
let id      = Symbol("id");   // Symbol (unique identifier)
```

### Reference Types

```js
let arr = [1, 2, 3];              // Array
let obj = { name: "Ali", age: 25 }; // Object
let fn  = function() {};          // Function
```

### `typeof` Operator

```js
typeof "hello"     // "string"
typeof 42          // "number"
typeof true        // "boolean"
typeof undefined   // "undefined"
typeof null        // "object"  ⚠️ known JS bug
typeof {}          // "object"
typeof []          // "object"
typeof function(){} // "function"
```

---

## 🔄 Type Coercion

JS automatically converts types in some operations.

```js
// Implicit coercion
"5" + 2       // "52"  — number converted to string
"5" - 2       // 3     — string converted to number
true + 1      // 2
false + 1     // 1
null + 1      // 1
undefined + 1 // NaN

// Explicit conversion
Number("42")   // 42
String(42)     // "42"
Boolean(0)     // false
Boolean("")    // false
Boolean("hi")  // true
parseInt("42px") // 42
parseFloat("3.14") // 3.14
```

### Truthy & Falsy Values

```js
// Falsy (6 values)
false, 0, "", null, undefined, NaN

// Everything else is truthy
"0", [], {}, -1, "false"  // all TRUTHY
```

---

## == vs ===

```js
// == loose equality (allows type coercion)
"5" == 5      // true
null == undefined // true

// === strict equality (no coercion)
"5" === 5     // false
null === undefined // false
```

> Always prefer `===` in real code.

---

## 📝 Interview Questions

**Q1. What is the difference between `var`, `let`, and `const`?**
> `var` is function-scoped and hoisted. `let` and `const` are block-scoped. `const` cannot be reassigned after declaration. Prefer `const` by default, use `let` when reassignment is needed, avoid `var`.

**Q2. What is the difference between `null` and `undefined`?**
> `undefined` means a variable was declared but not assigned a value. `null` is an explicit assignment meaning "no value" — it's intentional emptiness.

**Q3. Why does `typeof null` return `"object"`?**
> It's a long-standing bug in JavaScript from its early days. `null` is a primitive, not an object, but the type tag used internally was 0 (same as objects). It was never fixed to maintain backward compatibility.

**Q4. What is the difference between `==` and `===`?**
> `==` checks equality with type coercion (converts types before comparing). `===` checks both value AND type with no conversion. Always use `===` to avoid unexpected behavior.

**Q5. What are falsy values in JavaScript?**
> `false`, `0`, `""` (empty string), `null`, `undefined`, and `NaN`. All other values are truthy — including `"0"`, `[]`, and `{}`.

**Q6. What is type coercion? Give an example.**
> JavaScript automatically converts one type to another when needed. Example: `"5" - 2` = `3` (string converted to number), but `"5" + 2` = `"52"` (number converted to string because `+` also concatenates).

**Q7. What is the Temporal Dead Zone (TDZ)?**
> `let` and `const` are hoisted but not initialized. Accessing them before their declaration throws a `ReferenceError`. The period between entering the scope and the declaration is called the Temporal Dead Zone.

---

*Next: Operators & Control Flow →*