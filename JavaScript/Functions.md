# Functions

### Regular Function (Function Declaration):

```javascript
function greet() {
  console.log("Hello there!");
}
greet(); // to call function
```

### Regular Function (Function Expression):

```javascript
const speak = function () {
  console.log("Hello there!");
};
speak(); // to call function
```

### Arrow Function:

```javascript
// with no parameters
const fun = () => "Hello Wordl!";
const result = fun();
console.log(result);

// with one parameter and one return statement
const calcArea = (radius) => 3.14 * radius ** 2;
const result = calcArea();
console.log(result);

// with multiple parameters
const add = (num1, num2) => {
  console.log("Sum = " + num1 + num2);
};
add(5, 5);
```

### Default Parameter Value

```javascript
// Ex-1.
function add(num1 = 2, num2 = 4) {
  return num1 + num2;
}
add(5, 5);
// This function will take 2 and 4 as a default value. So whenever the values are not assed by user in calling function then it will use default values. Otherwise it will always take values that are passed in calling function.

// Ex-2.
function myFunction(x, y = 10) {
  // y is 10 if not passed or undefined
  return x + y;
}
myFunction(5); // will return 15
```

### Function Rest Parameter:

- The rest parameter (...) allows a function to treat an indefinite number of arguments as an array:

```javascript
function sum(...args) {
  let sum = 0;
  for (let arg of args) sum += arg;
  return sum;
}

let x = sum(4, 9, 16, 25, 29, 100, 66, 77);
```
