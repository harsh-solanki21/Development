## Callback Functions

- In JavaScript, a callback function is a function that is passed into another function as an argument.
- This function can then be invoked during the execution of that higher order function (that it is an argument of).
- Since, in JavaScript, functions are objects, functions can be passed as arguments.

The benefit of using a callback function is that you can wait for the result of a previous function call and then execute another function call.

```javascript
// Example 1:
function handleName(name, cb) {
  const fullName = `${name} Doe`;
  cb(fullName);
}

function makeUppercase(value) {
  console.log(value.toUpperCase());
}

handleName("John", makeUpperCase);

// Exmaple 2:
function compute(action, x, y) {
  if (action === "divide") {
    return x / y;
  } else if (action === "multiply") {
    return x * y;
  } else if (action === "add") {
    return x + y;
  } else if (action === "modulus") {
    return x % y;
  }
}

console.log(compute("divide", 10, 5)); // 2
console.log(compute("multiply", 10, 5)); // 50
console.log(compute("add", 10, 5)); // 15
console.log(compute("modulus", 10, 5)); // 0

// We can rewrite the above code in a better way as shown below.

function divide(x, y) {
  return x / y;
}

function multiply(x, y) {
  return x * y;
}

function computeOp(callBack, x, y) {
  return callBack(x, y);
}

console.log(computeOp(divide, 10, 5)); // 2
console.log(computeOp(multiply, 10, 5)); // 50
```
