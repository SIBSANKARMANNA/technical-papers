# JavaScript Fundamentals — Technical Revision

# 1. JavaScript Data Types

JavaScript has primitive and reference types.

### Primitive

```js
const name = "Rahul"; // string
const age = 25; // number
const isActive = true; // boolean
const value = undefined; // undefined
const user = null; // null
const bigNumber = 123n; // bigint
const id = Symbol("id"); // symbol
```

### Reference types

```js
const user = { name: "Rahul" };
const numbers = [10, 20, 30];
const greet = function () {};
```

Arrays and functions are objects.

Use `typeof` to check a value's type:

```js
typeof value;
Array.isArray(value);
```

> Note: `typeof null` returns `"object"` because of a historical JavaScript behavior.

---

# 2. Scope

Scope defines where a variable can be accessed.

Main types:

- Global scope
- Function scope
- Block scope
- Module scope

```js
function calculate() {
  const price = 100;

  if (price > 50) {
    const discount = 10;
  }

  // discount is not accessible here
}
```

`let` and `const` are block-scoped, while `var` is function-scoped.

---

# 3. `var`, `let`, and `const`

- `var` has function scope, can be reassigned, and can be redeclared.
- `let` has block scope and can be reassigned but not redeclared in the same scope.
- `const` has block scope and cannot be reassigned or redeclared.

```text
Use const by default.
Use let when reassignment is required.
Avoid var in modern JavaScript.
```

`const` does not make an object immutable:

```js
const user = { name: "Rahul" };

user.name = "Amit"; // allowed
```

---

# 4. Why Avoid `var`?

`var` can escape a block and can also be redeclared accidentally.

```js
if (true) {
  var score = 100;
}

console.log(score); // 100
```

```js
var count = 10;
var count = 20; // allowed
```

`let` and `const` prevent these problems through block scope and redeclaration rules.

---

# 5. Why Global Variables Are Bad

Global variables can be accessed and changed from many places, which makes code harder to understand, test, and debug.

Avoid:

```js
let total = 0;

function add(price) {
  total += price;
}
```

Prefer passing values into functions and returning results:

```js
function add(total, price) {
  return total + price;
}
```

This reduces accidental changes and makes functions easier to reuse and test.

---

# 6. Truthy and Falsy Values

Falsy values are:

```text
false
0
-0
0n
""
null
undefined
NaN
```

Everything else is truthy, including:

```js
[];
{
}
```

Be careful with:

```js
if (!value) {
  // 0, "", false, null and undefined all enter here
}
```

If you specifically want to check for `undefined`:

```js
if (value === undefined) {
  // ...
}
```

Use the condition that matches what you actually want to check.

---

# 7. Function Hoisting

Function declarations are hoisted:

```js
greet();

function greet() {
  console.log("Hello");
}
```

But function expressions and arrow functions assigned to `let`/`const` cannot be used before initialization:

```js
greet();

const greet = () => {
  console.log("Hello");
};
```

For readability, declare functions before using them instead of depending on hoisting.

---

# 8. Function Without `return`

A function that does not return a value returns `undefined`.

```js
function greet() {
  console.log("Hello");
}

const result = greet();

console.log(result); // undefined
```

`console.log()` displays a value; `return` sends a value back to the caller.

---

# 9. Ways to Declare Functions

### Function declaration

```js
function add(a, b) {
  return a + b;
}
```

### Function expression

```js
const add = function (a, b) {
  return a + b;
};
```

### Named function expression

```js
const add = function calculate(a, b) {
  return a + b;
};
```

### Arrow function

```js
const add = (a, b) => a + b;
```

Function declarations are hoisted; function expressions and arrow functions depend on the variable declaration.

---

# 10. Passing Functions to Other Functions

Functions are values, so they can be passed as arguments.

```js
function execute(callback) {
  callback();
}

function greet() {
  console.log("Hello");
}

execute(greet);
```

Notice the difference:

```js
execute(greet); // passes the function
execute(greet()); // calls it immediately
```

This idea is used heavily with callbacks, array methods, event handlers, and asynchronous code.

---

# 11. Named vs Anonymous Functions

A named function has its own name:

```js
function calculateTotal() {}
```

An anonymous function has no function name:

```js
const calculateTotal = function () {};
```

Named functions can make stack traces and debugging easier, especially for larger pieces of logic.

---

# 12. Variable Number of Arguments

Use the rest parameter when a function should accept any number of arguments.

```js
function addNumbers(...numbers) {
  return numbers.reduce((total, number) => total + number, 0);
}

addNumbers(10, 20, 30); // 60
```

`...numbers` collects the arguments into an array.

---

# 13. Pass by Value and Objects

JavaScript passes arguments by value.

For primitives, the function receives a copy of the value:

```js
let age = 25;

function changeAge(value) {
  value = 30;
}

changeAge(age);

console.log(age); // 25
```

For objects, the copied value is a reference to the same object:

```js
const user = { name: "Rahul" };

function changeName(person) {
  person.name = "Amit";
}

changeName(user);

console.log(user.name); // Amit
```

But reassigning the parameter does not replace the original object:

```js
function replaceUser(person) {
  person = { name: "Amit" };
}

replaceUser(user);

console.log(user.name); // Rahul
```

---

# 14. Loops

### Traditional `for`

Use when you need an index or precise loop control.

```js
for (let index = 0; index < numbers.length; index++) {
  console.log(numbers[index]);
}
```

### `for...of`

Use to iterate over values:

```js
for (const number of numbers) {
  console.log(number);
}
```

### `for...in`

Mainly useful for object keys:

```js
for (const key in user) {
  console.log(key, user[key]);
}
```

Avoid using `for...in` for normal array iteration.

### `forEach`

Use when you want to perform an action for every item:

```js
users.forEach((user) => {
  console.log(user.name);
});
```

### `while`

Useful when the number of iterations depends on a condition:

```js
while (attempts < 3) {
  attempts++;
}
```

---

# 15. Searching MDN

MDN is useful when you need to understand an API instead of memorizing everything.

Search for:

```text
MDN Array.map
MDN Array.splice
MDN JavaScript closures
MDN try catch
MDN arrow functions
```

When checking a method, look at:

- Parameters
- Return value
- Whether it mutates the original value
- Exceptions
- Examples

The goal is to learn how to find reliable documentation, not memorize every method.

---

<!-- rename again -->

# 16. Spread Operator

Spread expands arrays or object properties.

### Array

```js
const combined = [...first, ...second];
```

### Object

```js
const updatedUser = {
  ...user,
  age: 26,
};
```

Spread creates a **shallow copy**, not a deep copy.

For nested objects:

```js
const user = {
  name: "Rahul",
  address: {
    city: "Bengaluru",
  },
};

const copy = { ...user };

copy.address.city = "Mumbai";

console.log(user.address.city); // Mumbai
```

The nested object is still shared.

---

# 17. Template Literals

Use backticks when you need interpolation or multiline strings.

```js
const name = "Rahul";
const age = 25;

const message = `My name is ${name} and I am ${age} years old.`;
```

Expressions can also be used:

```js
const total = `Total: ${price * quantity}`;
```

---

# 18. Default Parameters

Default parameters provide a value when an argument is `undefined`.

```js
function greet(name = "Guest") {
  return `Hello ${name}`;
}

greet(); // Hello Guest
greet(undefined); // Hello Guest
greet(null); // Hello null
```

The default is not used for `null`, `false`, `0`, or an empty string.

---

# 19. Destructuring

Destructuring extracts values from arrays or objects.

### Array

```js
const [first, second] = numbers;
```

### Object

```js
const { name, age } = user;
```

Rename a property:

```js
const { name: userName } = user;
```

It is also useful in function parameters:

```js
function showUser({ name, age }) {
  console.log(name, age);
}
```

---

# 20. Closures

A closure allows an inner function to remember variables from its outer scope even after the outer function has finished.

```js
function createCounter() {
  let count = 0;

  return () => ++count;
}

const counter = createCounter();

counter(); // 1
counter(); // 2
counter(); // 3
```

Closures are useful for:

- Private state
- Counters
- Callbacks
- Function factories
- Maintaining state between calls

---

# 21. Arrow Functions vs Regular Functions

Arrow functions provide shorter syntax:

```js
const add = (a, b) => a + b;
```

The important difference is `this`.

Regular functions get their `this` based on how they are called:

```js
const user = {
  name: "Rahul",

  greet() {
    console.log(this.name);
  },
};
```

Arrow functions do not have their own `this`; they use `this` from the surrounding scope.

Therefore, don't use an arrow function as an object method when you need the object's `this`.

Arrow functions are especially common for callbacks:

```js
const doubled = numbers.map((number) => number * 2);
```

---

# 22. `===` vs `==`

Prefer `===` because it compares values without normal type coercion.

```js
5 === "5"; // false
5 == "5"; // true
```

Using `===` makes comparisons more predictable.

---

# 23. `null` vs `undefined`

### `undefined`

Usually means a value has not been provided or assigned.

```js
let username;

console.log(username); // undefined
```

A missing object property also returns `undefined`.

### `null`

Usually represents an intentionally empty value.

```js
let currentUser = null;
```

Simple way to remember:

```text
undefined -> no value was provided/assigned
null      -> intentionally no value
```

---

# 24. CommonJS Modules

CommonJS allows Node.js code to be split into separate files.

### Export

```js
// math.js

function add(a, b) {
  return a + b;
}

module.exports = { add };
```

### Import

```js
// app.js

const { add } = require("./math");

console.log(add(10, 20));
```

For a single exported value:

```js
module.exports = greet;
```

and:

```js
const greet = require("./greet");
```

---

# 25. Console Methods

Useful console methods:

```text
console.log()      -> general output
console.error()    -> errors
console.warn()     -> warnings
console.info()     -> information
console.table()    -> arrays/objects in table form
console.time()     -> start a timer
console.timeEnd()  -> end a timer
console.trace()    -> show stack trace
```

For debugging arrays of objects, `console.table()` is often easier to read than `console.log()`.

---

# 26. JavaScript Best Practices

- Use meaningful variable and function names.
- Prefer `const`; use `let` only when reassignment is needed.
- Avoid `var` in modern JavaScript.
- Use consistent `camelCase` naming.
- Use meaningful loop variables such as `user`, `student`, or `product`.
- Keep indentation and formatting consistent.
- Keep functions focused on one responsibility.
- Avoid unnecessary global variables.
- Don't hide errors with empty `catch` blocks.
- Use comments to explain **why**, not obvious code.
- Prefer readable code over unnecessarily clever code.

Example:

```js
function calculateTotal(items) {
  let total = 0;

  for (const item of items) {
    total += item.price;
  }

  return total;
}
```

---

# 27. Debugging Strategy

1. Read the error: Understand the error type and message.
2. Find the location: Check the file, line, and column from the stack trace.
3. Inspect values: Use `console.log()`, `console.table()`, `typeof`, and `Array.isArray()`.
4. Isolate the problem: Break large operations into smaller steps.
5. Fix the root cause: Don't simply hide the error with `catch`.

---
