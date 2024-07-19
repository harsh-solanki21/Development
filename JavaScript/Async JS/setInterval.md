# setInterval

- The setInterval() method repeats a block of code at every given timing event.

```javascript
// Example 1: Display a Text Once Every 1 Second
function greet() {
  console.log("Hello world");
}

setInterval(greet, 1000);

// Example 2: Display Time Every 5 Seconds
function showTime() {
  const dateTime = new Date();
  const time = dateTime.toLocaleTimeString();
  console.log(time);
}

setInterval(showTime, 5000);

// Example 3: Use clearInterval() Method
// program to stop the setInterval() method after five times
let count = 0;
const interval = setInterval(function () {
  count += 1;
  if (count === 5) {
    clearInterval(interval);
  }

  const dateTime = new Date();
  const time = dateTime.toLocaleTimeString();
  console.log(time);
}, 2000);

// Example 4: program to display a name
function greet(name, lastName) {
  console.log("Hello" + " " + name + " " + lastName);
}
// passing argument to setInterval
setInterval(greet, 1000, "John", "Doe");
```
