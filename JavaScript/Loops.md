# Loops

### 1. For

- The most common type of loop.

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}
// Output: 0, 1, 2, 3, 4
```

### 2. While

- Executes a block of code while a specified condition is true.

```javascript
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}
// Output: 0, 1, 2, 3, 4
```

### 3. Do...While

- Similar to while loop, but always executes the code block at least once.

```javascript
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);
// Output: 0, 1, 2, 3, 4
```

### 4. forEach

- A method on arrays to execute a provided function once for each array element.

```javascript
const arr = [1, 2, 3];
arr.forEach((item, index) => {
  console.log(`${index}: ${item}`);
});
// Output: "0: 1", "1: 2", "2: 3"
```

### 5. For...In

- Iterates over the enumerable properties of an object.

```javascript
const obj = { a: 1, b: 2, c: 3 };
for (let prop in obj) {
  console.log(`${prop}: ${obj[prop]}`);
}
// Output: "a: 1", "b: 2", "c: 3"
```

### 6. For...Of

- Iterates over iterable objects (arrays, strings, etc.).

- The JavaScript for/of statement loops through the values of an iterable objects.
  for/of lets you loop over data structures that are iterable such as Arrays, Strings, Maps, NodeLists, and more.

```javascript
// Looping over an array
const numbers = [1, 2, 3, 4, 5];
for (const num of numbers) {
  console.log(num);
}
// Output: 1, 2, 3, 4, 5

// Looping over a strig
const str = "Hello";
for (const char of str) {
  console.log(char);
}
// Output: H, e, l, l, o

// Looping over a Map
const myMap = new Map([
  ["a", 1],
  ["b", 2],
  ["c", 3],
]);
for (const [key, value] of myMap) {
  console.log(`${key}: ${value}`);
}
// Output: a: 1, b: 2, c: 3

// Looping over NodeList (DOM elements)
// Assuming we have multiple <p> elements in the HTML
const paragraphs = document.querySelectorAll("p");
for (const p of paragraphs) {
  console.log(p.textContent);
}
// Output: Content of each paragraph
```

### 7. map()

- Creates a new array with the results of calling a provided function on every element in the array.

```javascript
const arr = [1, 2, 3];
const doubled = arr.map((item) => item * 2);
console.log(doubled);
// Output: [2, 4, 6]
```
