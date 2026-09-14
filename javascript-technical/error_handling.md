# 9. Error Handling

Use `try...catch` when an operation can throw an error and your code can meaningfully handle it.

```js
try {
  const data = JSON.parse(input);
} catch (error) {
  console.error("Invalid JSON:", error.message);
}
```

`finally` is useful for cleanup and runs whether an error occurs or not.

```js
try {
  // operation
} catch (error) {
  console.error(error);
} finally {
  // cleanup
}
```

---

# 10. Throwing Errors

Use `throw` when your code needs to report an invalid situation.

```js
function withdraw(balance, amount) {
  if (amount > balance) {
    throw new Error("Insufficient balance");
  }

  return balance - amount;
}
```

Handle it with `try...catch` when appropriate.

---

# 11. `throw new Error()` vs Throwing a String

Prefer:

```js
throw new Error("Something went wrong");
```

Avoid:

```js
throw "Something went wrong";
```

`Error` provides useful debugging information:

```js
error.name;
error.message;
error.stack;
```

This makes errors easier to inspect and trace.

---

# 12. Reading Stack Traces

Stack traces are one of the most useful debugging tools.

Example:

```text
TypeError: Cannot read properties of undefined
    at calculateTotal (cart.js:15:20)
    at checkout (checkout.js:30:5)
```

Read it in this order:

```text
1. Error type
2. Error message
3. File name
4. Line number
5. Column number
6. Function where it happened
```

For:

```text
cart.js:15:20
```

it means:

```text
file   -> cart.js
line   -> 15
column -> 20
```

Then inspect the values involved around that location.

---

# 13. Stack Trace Practice — 2 Weeks

Practice debugging for around 15–20 minutes every day.

```text
Day 1  -> ReferenceError
Day 2  -> TypeError
Day 3  -> SyntaxError
Day 4  -> undefined values
Day 5  -> wrong function arguments
Day 6  -> array mistakes
Day 7  -> nested function errors
Day 8  -> map() errors
Day 9  -> filter() errors
Day 10 -> reduce() errors
Day 11 -> JSON errors
Day 12 -> try/catch
Day 13 -> custom errors
Day 14 -> debug a complete broken program
```

For every error, ask:

```text
What failed?
Where did it fail?
What value caused it?
Why did that value have that value/type?
What is the smallest correct fix?
```

First understand the error; then search if you still need help.

---

# 14. Importance of `catch`

A `catch` block should handle or report an error meaningfully.

Bad:

```js
try {
  riskyOperation();
} catch (error) {
  // ignore
}
```

Better:

```js
try {
  riskyOperation();
} catch (error) {
  console.error(error);
}
```

Never use `catch` simply to hide a problem.

---
