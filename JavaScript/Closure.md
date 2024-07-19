# Closure

- A closure is the combination of a function bundled together with references to its surrounding state(the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function.

```javascript
// Example 1:
function fun1() {
  let message = "Good Morning";
  function fun2() {
    console.log(message);
  }
}

// Example 2:
function init() {
  let name = "Harsh"; // name is a local variable created by init
  function displayName() {
    // this is an inner function, a closure
    console.log(name); // use variable declared in the parent function
  }
  name = "Solanki"; // this will change the value of name
  return displayName;
}

let c = init();
c();
```
