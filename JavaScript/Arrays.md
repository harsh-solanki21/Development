# Arrays

- var is function scoped and let is block scoped.
- Variables are pass by value.
- Objects are pass by reference.

```javascript
const fruits = ["banana", "apple", "orange", "pineapple"];
console.log(fruits[2]); // access value at index 2
fruits[0] = "pear";
console.log(fruits);

for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}

// Array Functions
console.log("to string", fruits.toString());
console.log(fruits.join(" * "));
console.log(fruits.pop(), fruits); //removes last element from the array
console.log(fruits.push("blackbarries"), fruits); //appends at the last
fruits.shift(); //remove first element from the array
fruits.unshift("kiwi"); //add element to the first in array
fruits.push("kiwi"); //add element to the last in array
fruits.includes("banana"); //returns true if array includes banana element, otherwise returns false

let vegetables = ["asparagus", "tomato", "broccoli"];
let allGroceries = fruits.concate(vegetables); //this will concate both the arrays
//The concat() method does not change the existing arrays. It always returns a new array.

console.log(allGroceries.slice(1, 4));
allGroceries.reverse();
allGroceries.sort();

let somenumers = [5, 10, 2, 25, 3, 255, 1, 2];
console.log(
  someNumbers.sort(function (a, b) {
    return a - b;
  })
); //sort in ascending order
console.log(
  someNumbers.sort(function (a, b) {
    return b - a;
  })
); //sort in descending order

let emptyArray = new Array(); //object array
for (let i = 1; i <= 10; i++) {
  emptyArray.push(i);
}
console.log(emptyArray);
// always try to use normal array and not object array

// splice() method can be used to add new items to an array:
let fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 0, "Lemon", "Kiwi");
fruits.splice(0, 1); // Removes the first element of fruits

// The first parameter (2) defines the position where new elements should be added (spliced in).
// The second parameter (0) defines how many elements should be removed.
// The rest of the parameters ("Lemon" , "Kiwi") define the new elements to be added.
// The splice() method returns an array with the deleted items.

Array.forEach(); // to iterate through all the elements of an array
Array.every(); // to check(condition) for every element in an array
```
