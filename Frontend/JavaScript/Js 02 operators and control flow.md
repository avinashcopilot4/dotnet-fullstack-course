# JavaScript – Operators & Control Flow

---

## ➕ Operators

### Arithmetic
```js
5 + 2   // 7
5 - 2   // 3
5 * 2   // 10
5 / 2   // 2.5
5 % 2   // 1  (modulus — remainder)
5 ** 2  // 25 (exponentiation)
```

### Assignment
```js
let x = 10;
x += 5;   // x = 15
x -= 3;   // x = 12
x *= 2;   // x = 24
x /= 4;   // x = 6
x **= 2;  // x = 36
x %= 5;   // x = 1
```

### Comparison
```js
5 > 3     // true
5 < 3     // false
5 >= 5    // true
5 <= 4    // false
5 === 5   // true  (strict)
5 !== "5" // true  (strict not-equal)
```

### Logical
```js
true && false   // false  (AND)
true || false   // true   (OR)
!true           // false  (NOT)
```

### Short-Circuit Evaluation
```js
// && returns first falsy or last value
null && "hello"   // null
"hi" && "world"   // "world"

// || returns first truthy or last value
null || "default"   // "default"
"value" || "default" // "value"

// ?? Nullish coalescing — returns right side only for null/undefined
null ?? "default"      // "default"
0    ?? "default"      // 0  (0 is NOT null/undefined)
""   ?? "default"      // "" (empty string is NOT null/undefined)
```

### Ternary Operator
```js
let status = age >= 18 ? "adult" : "minor";
```

### Optional Chaining `?.`
```js
let user = null;
user?.name          // undefined (no error)
user?.address?.city // undefined (no error)
arr?.[0]            // safe array access
fn?.()              // safe function call
```

---

## 🔀 Control Flow

### if / else if / else
```js
let score = 75;

if (score >= 90) {
  console.log("A grade");
} else if (score >= 70) {
  console.log("B grade");
} else {
  console.log("C grade");
}
```

### switch
```js
let day = "Monday";

switch (day) {
  case "Saturday":
  case "Sunday":
    console.log("Weekend");
    break;
  case "Monday":
    console.log("Weekday");
    break;
  default:
    console.log("Unknown");
}
```

---

## 🔁 Loops

### for
```js
for (let i = 0; i < 5; i++) {
  console.log(i);  // 0 1 2 3 4
}
```

### while
```js
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}
```

### do...while (always runs at least once)
```js
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);
```

### for...of (iterate over values)
```js
const fruits = ["apple", "banana", "mango"];
for (const fruit of fruits) {
  console.log(fruit);
}
```

### for...in (iterate over object keys)
```js
const user = { name: "Ali", age: 25 };
for (const key in user) {
  console.log(key, user[key]);  // name Ali / age 25
}
```

### break & continue
```js
for (let i = 0; i < 10; i++) {
  if (i === 3) continue;  // skip 3
  if (i === 7) break;     // stop at 7
  console.log(i);         // 0 1 2 4 5 6
}
```

---

## 📝 Interview Questions

**Q1. What is the difference between `&&` and `||`?**
> `&&` (AND) returns the first falsy value or the last value if all are truthy. `||` (OR) returns the first truthy value or the last value if all are falsy. Both short-circuit — they stop evaluating as soon as the result is determined.

**Q2. What is the nullish coalescing operator `??` and how is it different from `||`?**
> `??` only returns the right-hand side if the left is `null` or `undefined`. `||` returns the right side for any falsy value (including `0`, `""`, `false`). Use `??` when `0` or empty string are valid values.

**Q3. What is optional chaining `?.` and when would you use it?**
> It safely accesses nested properties without throwing an error if the chain is `null` or `undefined`. Instead of an error, it returns `undefined`. Use it when accessing data from APIs where nested properties might be missing.

**Q4. What is the difference between `for...of` and `for...in`?**
> `for...of` iterates over **values** of an iterable (arrays, strings). `for...in` iterates over **keys/property names** of an object. Using `for...in` on arrays is not recommended because it can include inherited properties.

**Q5. What is short-circuit evaluation?**
> JS stops evaluating a logical expression as soon as the result is certain. In `a && b`, if `a` is falsy, `b` is never evaluated. In `a || b`, if `a` is truthy, `b` is never evaluated. This is useful for conditional execution and default values.

**Q6. What is the difference between `while` and `do...while`?**
> `while` checks the condition *before* executing — the body may never run. `do...while` checks the condition *after* — the body always runs at least once.

**Q7. What does `break` vs `continue` do in a loop?**
> `break` exits the loop entirely. `continue` skips the current iteration and moves to the next one.

---

*Next: Functions →*