# 1. Array Utility Methods

## Basic methods

- push() adds an element to the end of an array and mutates the original array.
- pop() removes the last element and mutates the array.
- concat() combines arrays and returns a new array without changing the originals.
- slice() extracts part of an array and returns a new array.
- splice() can add or remove elements but changes the original array.
- join() converts an array to a string, while flat() creates a new flattened array.

Remember:

```text
slice  -> returns a portion without changing the array
splice -> changes the original array
```

---

# 2. Array Finding Methods

### `find()`

Returns the first matching element, or `undefined`.

```js
const user = users.find((user) => user.id === 2);
```

### `findIndex()`

Returns the index of the first matching element, or `-1`.

```js
const index = numbers.findIndex((number) => number === 20);
```

### `indexOf()`

Finds the index of a value:

```js
numbers.indexOf(20);
```

### `includes()`

Checks whether an array contains a value:

```js
roles.includes("admin");
```

Use `find()` when you need the object/value, and `findIndex()` when you need its position.

---

# 3. Higher-Order Array Methods

### `forEach()`

Use when you want to perform an action and don't need a returned array.

```js
users.forEach((user) => {
  console.log(user.name);
});
```

`forEach()` itself returns `undefined`.

### `map()` — non-mutating

Use when every item should produce a new value.

```js
const names = users.map((user) => user.name);
```

### `filter()` — non-mutating

Use when you want only items that satisfy a condition.

```js
const adults = users.filter((user) => user.age >= 18);
```

### `reduce()` — non-mutating

Use when multiple values need to be combined into one result.

```js
const total = prices.reduce((sum, price) => sum + price, 0);
```

### `sort()` — mutating

`sort()` changes the original array.

For numbers, provide a comparison function:

```js
numbers.sort((a, b) => a - b);
```

---

# 4. Array Method Chaining

Array methods can be combined when each step produces the input required by the next step.

```js
const result = products
  .filter((product) => product.available)
  .map((product) => product.price)
  .reduce((total, price) => total + price, 0);
```

Think of it as:

```text
filter -> select
map    -> transform
reduce -> combine
```

Keep chains readable. If a chain becomes difficult to understand, split it into separate variables.

---

# 5. Mutable vs Immutable Array Methods

### Common mutating methods

```text
push()
pop()
splice()
sort()
shift()
unshift()
reverse()
fill()
```

### Common non-mutating methods

```text
concat()
slice()
map()
filter()
reduce()
find()
findIndex()
includes()
indexOf()
join()
flat()
```

Modern alternatives:

```js
toSorted();
toReversed();
toSpliced();
```

These return new arrays instead of modifying the original.

---

# 6. String Utility Methods

Strings are immutable, so string methods return new values instead of changing the original string.

Common methods:

```text
toUpperCase()
toLowerCase()
trim()
includes()
startsWith()
endsWith()
slice()
replace()
replaceAll()
split()
charAt()
```

Example:

```js
const message = "  Hello Rahul  ";

const result = message.trim().toUpperCase().replace("RAHUL", "AMIT");

console.log(result); // HELLO AMIT
console.log(message); // unchanged
```

---

# 7. Object Utility Methods

For:

```js
const user = {
  name: "Rahul",
  age: 25,
};
```

### `Object.keys()`

Returns property names.

```js
Object.keys(user);
```

### `Object.values()`

Returns property values.

```js
Object.values(user);
```

### `Object.entries()`

Returns key-value pairs and is useful for iteration.

```js
for (const [key, value] of Object.entries(user)) {
  console.log(key, value);
}
```

### `Object.hasOwn()`

Checks whether an object directly contains a property.

```js
Object.hasOwn(user, "name");
```

### `Object.assign()`

Copies properties into a target object and mutates that target.

```js
Object.assign(target, source);
```

For a simple shallow copy, object spread is usually clearer:

```js
const copy = { ...user };
```

### `Object.freeze()`

Prevents changes to an object at the top level.

```text
Object.freeze() is shallow.
```

Nested objects can still be changed unless they are also frozen.

---

# 8. Choosing `forEach`, `map`, `filter`, and `reduce`

```text
forEach -> perform an action
map     -> transform every item
filter  -> select matching items
reduce  -> combine values into one result
```

Example:

```js
const names = users.filter((user) => user.active).map((user) => user.name);
```

Use the method that describes the intention of the operation instead of using `forEach()` for everything.

---
