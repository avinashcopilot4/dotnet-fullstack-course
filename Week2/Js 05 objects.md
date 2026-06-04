# JavaScript – Objects

---

## 📘 What is an Object?

An object is a **collection of key-value pairs** (properties and methods). Keys are strings (or Symbols), values can be anything.

```js
const user = {
  name: "Ali",
  age: 25,
  isAdmin: false,
  greet: function() {
    return "Hello, " + this.name;
  }
};

// Access properties
user.name         // "Ali"      (dot notation)
user["name"]      // "Ali"      (bracket notation — useful for dynamic keys)

// Call method
user.greet()      // "Hello, Ali"
```

---

## 🔧 Adding, Updating, Deleting

```js
const car = { brand: "Toyota" };

car.color = "red";      // add property
car.brand = "Honda";    // update property
delete car.color;       // remove property

// Check if property exists
"brand" in car          // true
car.hasOwnProperty("brand")  // true
```

---

## 🔑 Iterating Over Objects

```js
const user = { name: "Ali", age: 25, city: "Hyderabad" };

// for...in — keys
for (const key in user) {
  console.log(key, user[key]);
}

// Object.keys() — array of keys
Object.keys(user)     // ["name", "age", "city"]

// Object.values() — array of values
Object.values(user)   // ["Ali", 25, "Hyderabad"]

// Object.entries() — array of [key, value] pairs
Object.entries(user)  // [["name","Ali"], ["age",25], ["city","Hyderabad"]]
```

---

## 📦 ES6 Object Features

### Shorthand Properties
```js
const name = "Ali";
const age = 25;

// Old way
const user = { name: name, age: age };

// Shorthand
const user = { name, age };
```

### Computed Property Names
```js
const key = "name";
const obj = { [key]: "Ali" };  // { name: "Ali" }
```

### Method Shorthand
```js
const user = {
  name: "Ali",
  greet() {             // shorter than greet: function() {}
    return "Hi " + this.name;
  }
};
```

---

## 🔓 Destructuring

```js
const user = { name: "Ali", age: 25, city: "Hyderabad" };

// Basic
const { name, age } = user;
console.log(name);  // "Ali"

// Rename
const { name: userName } = user;
console.log(userName);  // "Ali"

// Default value
const { country = "India" } = user;
console.log(country);  // "India"

// Nested
const { address: { city } } = { address: { city: "Hyderabad" } };

// In function params
function display({ name, age }) {
  console.log(name, age);
}
display(user);
```

---

## 🌐 Spread & Rest with Objects

### Spread — copy or merge objects
```js
const defaults = { theme: "light", lang: "en" };
const settings = { ...defaults, lang: "te", fontSize: 14 };
// { theme: "light", lang: "te", fontSize: 14 }

// Shallow copy
const copy = { ...user };
```

### Rest — collect remaining properties
```js
const { name, age, ...rest } = { name: "Ali", age: 25, city: "Hyderabad" };
// rest = { city: "Hyderabad" }
```

---

## 🧱 Object Methods

```js
// Object.assign — merge objects (mutates target)
Object.assign({}, defaults, settings);

// Object.freeze — prevent modifications
const config = Object.freeze({ host: "localhost" });
config.host = "prod";  // silently fails (no error in non-strict)

// Object.keys / values / entries
Object.keys(user)
Object.values(user)
Object.entries(user)

// Object.fromEntries — convert entries back to object
const entries = [["name", "Ali"], ["age", 25]];
Object.fromEntries(entries)  // { name: "Ali", age: 25 }
```

---

## 🆚 Value vs Reference

```js
// Primitives — copied by value
let a = 10;
let b = a;
b = 20;
console.log(a);  // 10 (unchanged)

// Objects — copied by reference
let obj1 = { x: 1 };
let obj2 = obj1;
obj2.x = 99;
console.log(obj1.x);  // 99 (obj1 changed too!)

// Proper copy
let obj3 = { ...obj1 };  // shallow copy
```

---

## 📝 Interview Questions

**Q1. What is the difference between dot notation and bracket notation?**
> Dot notation (`obj.name`) is cleaner but requires valid identifiers. Bracket notation (`obj["name"]`) allows dynamic key access, keys with spaces, or keys stored in variables.

**Q2. What is the difference between pass by value and pass by reference?**
> Primitives (numbers, strings, booleans) are copied by value — changes don't affect the original. Objects and arrays are copied by reference — both variables point to the same memory location, so changes affect both.

**Q3. What does `Object.freeze()` do?**
> It prevents any modifications to an object — no adding, deleting, or changing properties. However, it is a **shallow** freeze — nested objects can still be modified.

**Q4. What is destructuring and why is it useful?**
> Destructuring extracts values from objects/arrays into variables with concise syntax. It's useful for function parameters, working with API responses, and avoiding repetitive `obj.prop` access.

**Q5. What is the difference between `Object.assign()` and spread `...`?**
> Both do a shallow copy/merge. `Object.assign(target, source)` mutates the target. Spread creates a new object without mutation. Spread is preferred in modern JS.

**Q6. What does `Object.entries()` return and when is it useful?**
> It returns an array of `[key, value]` pairs. Useful for iterating over objects with `forEach`/`map`, or converting to a `Map`, or filtering/transforming object properties.

**Q7. What is a shallow copy vs a deep copy?**
> A shallow copy copies only the top-level properties — nested objects are still references. A deep copy copies all levels. Use `structuredClone(obj)` or `JSON.parse(JSON.stringify(obj))` for deep copying (with limitations).

---

*Next: ES6+ Features →*