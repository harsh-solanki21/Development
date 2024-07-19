# Higher order functions

### 1. forEach()

- The .forEach() method executes a callback function on each of the elements in an array in order.

```javascript
const arr = ["a", "b", "c"];
arr.forEach((element) => console.log(element));
```

<br />

### 2. map()

- The `.map()` method executes a callback function on each element in an array. It returns a new array made up of the return values from the callback function.
- The original array does not get altered, and the returned array may contain different elements than the original array.

```javascript
const numbers = [1, 4, 9];
const doubles = numbers.map((num) => {
  return num * 2;
});

// doubles is now [2, 8, 18]
// numbers is still [1, 4, 9]

// we can do multiple operations
const ageMap = ages.map((age) => Math.sqrt(age)).map((age) => age * 2);
```

<br />

### 3. sort()

```javascript
let numbers = [4, 20, 5, 1, 3];
numbers.sort((a, b) => a - b);
console.log(numbers);
```

<br />

### 4. filter()

- The `.filter()` method executes a callback function on each element in an array.
- The callback function for each of the elements must return either true or false.
- The returned array is a new array with any elements for which the callback function returns true .

```javascript
// Ex-1.
const words = [
  "spray",
  "limit",
  "elite",
  "exuberent",
  "destruction",
  "present",
];
const result = words.filter((word) => {
  word.length > 6;
});
console.log(result);
// Output: ['exuberent', 'destruction', 'present']

// Ex-2.
function isAboveMyRange(value) {
  return value >= 25;
}
const filtered = [12, 5, 8, 130, 44].filter(isAboveMyRange);
// Output - [130, 44]
```

<br />

### 5. reduce()

- The `.reduce()` method iterates through an array and returns a single value.
- It takes a callback function with two parameters `(accumulator, currentValue)` as arguments. On each iteration, accumulator is the value returned by the last iteration, and the currentValue is the current element.
- Optionally, a second argument can be passed which acts as the initial value of the accumulator.

```javascript
const arr = [1, 2, 3, 4, 5];
const sum = arr.reduce((accumulator, currentValue) => {
  return ccumulator + currentValue;
});

console.log(sum); // 15
```

<br />

- It takes 2 numbers and does the operation for all numbers in the array (intuition can be like below)
  1, 2, 3, 4, 5
  3, 3, 4, 5
  6, 4, 5
  10, 5
  15

```javascript
const ages = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const combined = ages
  .map((age) => age * 2)
  .filter((age) => age > 10)
  .sort((a, b) => a - b)
  .reduce((a, b) => a + b, 0);

console.log(combined); // 80
```
