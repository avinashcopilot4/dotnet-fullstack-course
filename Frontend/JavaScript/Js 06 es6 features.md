# JavaScript – ES6+ Features

---

## 📘 Overview

ES6 (ECMAScript 2015) and beyond introduced major improvements to JavaScript. These features are used daily in modern JS and frameworks like React, Angular, and Vue.

---

## 🔤 Template Literals

```js
const name = "Ali";
const age = 25;

// Old way
const msg = "Hello, " + name + "! You are " + age + " years old.";

// Template literal
const msg = `Hello, ${name}! You are ${age} years old.`;

// Multi-line
const html = `
  <div>
    <h1>${name}</h1>
    <p>${age}</p>
  </div>
`;

// Expression
const result = `2 + 2 = ${2 + 2}`;
```

---

## 📦 Destructuring (Arrays & Objects)

```js
// Array destructuring
const [a, b, c] = [1, 2, 3];
const [first, , third] = [10, 20, 30];  // skip index 1
const [x, ...rest] = [1, 2, 3, 4];     // rest = [2, 3, 4]

// Swap variables
let m = 1, n = 2;
[m, n] = [n, m];

// Object destructuring
const { name, age = 18 } = { name: "Ali" };
const { name: userName } = { name: "Ali" };
```

---

## ↔️ Spread & Rest Operators `...`

```js
// Spread — expand an iterable
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];           // [1, 2, 3, 4, 5]
const copy = [...arr1];                 // shallow copy

Math.max(...arr1)                       // 3

// Spread objects
const merged = { ...obj1, ...obj2 };

// Rest — collect remaining items
function sum(...nums) {
  return nums.reduce((a, b) => a + b, 0);
}
```

---

## 🔢 Enhanced Object Literals

```js
const x = 10, y = 20;

const point = {
  x,                        // shorthand: x: x
  y,
  toString() {              // method shorthand
    return `(${this.x}, ${this.y})`;
  },
  ["key_" + x]: true       // computed property
};
```

---

## 🏭 Classes (ES6)

```js
class Animal {
  // Constructor
  constructor(name, sound) {
    this.name = name;
    this.sound = sound;
  }

  // Method
  speak() {
    return `${this.name} says ${this.sound}`;
  }

  // Static method (called on the class, not instance)
  static create(name, sound) {
    return new Animal(name, sound);
  }
}

// Inheritance
class Dog extends Animal {
  constructor(name) {
    super(name, "Woof");   // call parent constructor
    this.tricks = [];
  }

  learn(trick) {
    this.tricks.push(trick);
  }

  // Override parent method
  speak() {
    return super.speak() + "!";
  }
}

const dog = new Dog("Rex");
dog.speak();   // "Rex says Woof!"
```

### Getters & Setters
```js
class Circle {
  constructor(radius) {
    this._radius = radius;
  }

  get area() {
    return Math.PI * this._radius ** 2;
  }

  set radius(value) {
    if (value < 0) throw new Error("Negative radius");
    this._radius = value;
  }
}

const c = new Circle(5);
c.area;      // 78.53... (no parentheses needed)
c.radius = 10;
```

---

## 🗃️ Modules (import / export)

```js
// math.js — named exports
export const PI = 3.14;
export function add(a, b) { return a + b; }
export function subtract(a, b) { return a - b; }

// math.js — default export
export default function multiply(a, b) { return a * b; }

// app.js — import named
import { PI, add } from './math.js';

// app.js — import default
import multiply from './math.js';

// Import everything
import * as Math from './math.js';
Math.add(2, 3);

// Rename on import
import { add as sum } from './math.js';
```

---

## 🔣 Symbols

```js
const id = Symbol("id");
const id2 = Symbol("id");

id === id2  // false — always unique

const user = {
  [id]: 123,       // Symbol as key
  name: "Ali"
};

user[id]          // 123
```

---

## 🗺️ Map & Set

### Map (key-value, any type as key)
```js
const map = new Map();
map.set("name", "Ali");
map.set(42, "answer");
map.set(true, "yes");

map.get("name")     // "Ali"
map.has("name")     // true
map.size            // 3
map.delete("name")

// Iterate
for (const [key, value] of map) {
  console.log(key, value);
}
```

### Set (unique values)
```js
const set = new Set([1, 2, 2, 3, 3]);
// Set {1, 2, 3}

set.add(4);
set.has(2)   // true
set.size     // 4
set.delete(1);

// Remove duplicates from array
const unique = [...new Set([1, 2, 2, 3])];  // [1, 2, 3]
```

---

## 📝 Interview Questions

**Q1. What are template literals and what are their advantages?**
> Template literals use backticks and allow embedded expressions with `${}`, multi-line strings, and cleaner string concatenation. They eliminate the need for `+` operators in string building.

**Q2. What is the difference between `Map` and a plain object `{}`?**
> A `Map` can use any type as a key (objects, numbers), maintains insertion order, has a `.size` property, and is better for frequent additions/removals. Plain objects only support string/Symbol keys and don't have `.size`.

**Q3. What is the difference between `Set` and an Array?**
> A `Set` only stores **unique** values and has O(1) lookup with `.has()`. Arrays allow duplicates and have O(n) search. Use `Set` when uniqueness matters or fast membership checks are needed.

**Q4. What is the difference between `export default` and named exports?**
> Named exports allow multiple exports per file and must be imported with the exact name (or aliased). Default export is one per file and can be imported with any name. Both can coexist.

**Q5. What does the `super` keyword do in a class?**
> In a constructor, `super()` calls the parent class constructor and must be called before accessing `this`. In a method, `super.method()` calls the parent's version of that method — useful for extending behavior.

**Q6. What is a getter and setter in a class?**
> Getters (`get`) allow a method to be accessed like a property (no `()`). Setters (`set`) allow validation or side effects when a property is assigned. They provide controlled access to internal state.

**Q7. What is the difference between rest and spread — they both use `...`?**
> They look the same but work differently. **Spread** expands an iterable into individual elements (used in function calls or array/object literals). **Rest** collects multiple elements into a single array/object (used in function parameters or destructuring).

---

*Next: DOM Manipulation →*