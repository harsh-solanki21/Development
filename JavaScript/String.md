# Strings

```javascript
const s1 = "Hello";
console.log(typeof s1); // String

const s2 = new String("Hello");
console.log(typeof s2); // Object

// Never create string as an object. It slows down execution speed.

let fruit = "banana, apple, orange, kiwi, banana";

console.log(fruit.length); // returns length of string
fruit.indexOf("nan"); // returns the index of (the position of) the first occurrence of a specified text in a string
fruit.lastIndexOf("banana"); // returns the index of the last occurrence of a specified text in a string
// Both indexOf(), and lastIndexOf() return -1 if the text is not found.

fruit.search("kiwi"); // searches a string for a specified value and returns the position of the match
fruit.slice(2, 6); // extracts a part of a string and returns the extracted part in a new string.
fruit.substring(7, 13); // it will slice out the rest of the string.

// substring() is similar to slice().
// The difference is that substring() cannot accept negative indexes.

fruit.substr(7, 6);
// substr() is similar to slice(). it accepts negative values/
// The difference is that the second parameter specifies the length of the extracted part.

fruit.replace("ban", "123"); // replaces a specified value with another value in a string
// we can also use RegEx to replace
var str = " Hello World! ";
alert(str.replace(/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, ""));

fruit.toUpperCase(); // convert the string into uppercase letters
fruit.toLowerCase(); // convert the string into lowercase letters

// concate two or more variables:
let text = "Hello" + " " + "World!";
let text = "Hello".concat(" ", "World!");

// trim() method removes whitespace from both sides of a string:
let str = " Hello World! ";
alert(str.trim());

const string = "Harsh Solanki";
console.log(string.includes("an")); // returns true if string contains that text, otherwise returns false

// Extracting string characters
// The charAt() method returns the character at a specified index (position) in a string:
fruit.charAt(2);
fruit[2];

// The charCodeAt() method returns the unicode of the character at a specified index in a string:
let str = "HELLO WORLD";
str.charCodeAt(0); // returns 72

// Converting a string to an Array
// split() converts string into array.
fruit.split(","); // split by comma
fruit.split(" "); // split by space
fruit.split(""); // split by character
```
