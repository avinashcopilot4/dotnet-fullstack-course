# JavaScript – Arrays

---

## 📘 What is an Array?

An array is an **ordered list** of values. Arrays in JS can hold mixed types and are dynamic (no fixed size).

```js
const fruits = ["apple", "banana", "mango"];
const mixed  = [1, "hello", true, null, { id: 1 }];

// Access by index (0-based)
fruits[0]  // "apple"
fruits[2]  // "mango"

// Length
fruits.length  // 3

// Last element
fruits[fruits.length - 1]  // "mango"
fruits.at(-1)              // "mango" (ES2022)
```

---

## 🔧 Adding & Removing Elements

```js
const arr = [1, 2, 3];

// Add / Remove at END
arr.push(4);      // [1, 2, 3, 4] — returns new length
arr.pop();        // [1, 2, 3]    — returns removed element

// Add / Remove at START
arr.unshift(0);   // [0, 1, 2, 3] — returns new length
arr.shift();      // [1, 2, 3]    — returns removed element

// Add/Remove anywhere — splice(startIndex, deleteCount, ...items)
arr.splice(1, 0, 99);   // [1, 99, 2, 3]  — insert at index 1
arr.splice(1, 1);       // [1, 2, 3]      — remove 1 at index 1
arr.splice(1, 1, 55);   // [1, 55, 3]     — replace at index 1
```

---

## 🔍 Searching

```js
const arr = [10, 20, 30, 20];

arr.indexOf(20)          // 1 (first occurrence)
arr.lastIndexOf(20)      // 3
arr.includes(30)         // true
arr.find(n => n > 15)    // 20 (first match)
arr.findIndex(n => n > 15) // 1 (index of first match)
```

---

## 🔄 Iteration Methods

### forEach — just loop, no return
```js
[1, 2, 3].forEach(n => console.log(n));
```

### map — transform each element, returns NEW array
```js
const doubled = [1, 2, 3].map(n => n * 2);  // [2, 4, 6]
```

### filter — keep elements that pass a test, returns NEW array
```js
const evens = [1, 2, 3, 4].filter(n => n % 2 === 0);  // [2, 4]
```

### reduce — accumulate to a single value
```js
const sum = [1, 2, 3, 4].reduce((acc, n) => acc + n, 0);  // 10
// acc = accumulator (starts at 0), n = current element
```

### some — true if ANY element passes
```js
[1, 2, 3].some(n => n > 2);   // true
```

### every — true if ALL elements pass
```js
[2, 4, 6].every(n => n % 2 === 0);  // true
```

### flat & flatMap
```js
[1, [2, 3], [4, [5]]].flat()    // [1, 2, 3, 4, [5]]
[1, [2, 3], [4, [5]]].flat(2)   // [1, 2, 3, 4, 5] (depth 2)

[[1], [2], [3]].flatMap(a => a.map(n => n * 2))  // [2, 4, 6]
```

---

## 🔀 Sorting & Reversing

```js
// reverse (mutates original)
[1, 2, 3].reverse()   // [3, 2, 1]

// sort (mutates, default is string sort!)
["banana", "apple", "mango"].sort()  // alphabetical ✅

// ⚠️ Number sort needs a comparator
[10, 2, 30, 4].sort()             // [10, 2, 30, 4] ❌ (string sort!)
[10, 2, 30, 4].sort((a, b) => a - b)  // [2, 4, 10, 30] ✅ ascending
[10, 2, 30, 4].sort((a, b) => b - a)  // [30, 10, 4, 2]  descending
```

---

## 📋 Copying & Combining

```js
const a = [1, 2, 3];
const b = [4, 5, 6];

// Combine
a.concat(b)         // [1, 2, 3, 4, 5, 6]
[...a, ...b]        // [1, 2, 3, 4, 5, 6] (spread)

// Slice — extract without mutating (start inclusive, end exclusive)
a.slice(1, 3)       // [2, 3]
a.slice(-2)         // [2, 3] (last 2)

// Shallow copy
const copy = [...a];
const copy2 = a.slice();
const copy3 = Array.from(a);
```

---

## 🔃 Converting

```js
// Array to string
[1, 2, 3].join(", ")   // "1, 2, 3"
[1, 2, 3].join("")     // "123"

// String to array
"hello".split("")        // ["h","e","l","l","o"]
"a,b,c".split(",")       // ["a","b","c"]

// Check if array
Array.isArray([1, 2])    // true
Array.isArray("hello")   // false

// From iterable / array-like
Array.from("hello")      // ["h","e","l","l","o"]
Array.from({length: 3}, (_, i) => i)  // [0, 1, 2]
```

---

## 📝 Interview Questions

**Q1. What is the difference between `map` and `forEach`?**
> `map` returns a **new array** with transformed elements. `forEach` returns `undefined` — it's used for side effects only (logging, DOM updates). Never use `forEach` when you need a transformed array.

**Q2. What is the difference between `find` and `filter`?**
> `find` returns the **first element** that matches (single value or `undefined`). `filter` returns **all matching elements** in a new array (or an empty array if none match).

**Q3. What does `reduce` do? Give an example.**
> It reduces an array to a single value by running an accumulator function. Example: `[1,2,3,4].reduce((acc, n) => acc + n, 0)` → `10`. The second argument (`0`) is the initial accumulator value.

**Q4. What is the difference between `slice` and `splice`?**
> `slice` extracts a portion and returns a **new array** without modifying the original. `splice` **mutates** the original array — it can add, remove, or replace elements in place.

**Q5. Why does `.sort()` fail on numbers by default?**
> Because `.sort()` converts elements to strings by default. `[10, 2, 30].sort()` gives `[10, 2, 30]` as strings. Always pass a comparator for numbers: `.sort((a, b) => a - b)`.

**Q6. What is the difference between `push` and `concat`?**
> `push` mutates the original array and adds elements to the end. `concat` returns a new array with the elements combined and does not modify the original.

**Q7. How do you remove duplicates from an array?**
> Using `Set`: `[...new Set([1, 2, 2, 3])]` → `[1, 2, 3]`. A `Set` only stores unique values.

---

*Next: Objects →*