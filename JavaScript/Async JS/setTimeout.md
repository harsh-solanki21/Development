# setTimeout

- The setTimeout() method executes a block of code after the specified time.

```javascript
// Example 1: Display a Text Once After 3 Second
function greet() {
  console.log("Hello world");
}

setTimeout(greet, 3000);
console.log("This message is shown first");

// Example 2: setTimeout() method returns the interval id
function greet() {
  console.log("Hello world");
}

const intervalId = setTimeout(greet, 3000);
console.log("ID: " + intervalId);

// Example 3: Use clearTimeout() Method
let count = 0;
function increaseCount() {
  count += 1;
  console.log(count);
}

const id = setTimeout(increaseCount, 3000);
clearTimeout(id);
console.log("setTimeout is stopped.");

// Exmaple 4: Program to display a name
function greet(name, lastName) {
  console.log("Hello" + " " + name + " " + lastName);
}
// passing argument to setTimeout
setTimeout(greet, 1000, "John", "Doe");
```
