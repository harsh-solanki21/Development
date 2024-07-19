# JavaScript Best Practices

- Primitive types (numbers, string, boolean, null, undefined, symbols) are stored in Stack memory.

- Reference types (arrays, object literals, functions, dates, other objects) are stored in Heap memory.

- Because stack memory contains limited space but the Heap memory has more space. Objects takes more space in memory that's why it gets stored in Heap memory.

<br />

- Primitive types are stored by value.
- Reference types are stored by reference.

<br />

```javascript

Example:
// by value
let a = 10;
let b = a;
// Output: a = 20 and b = 10;
// This will create seperate space for both the variables even though they are same.
// When you update the value of a = 20 then it won't reflect in the value of b
// because they are stored as a different value in stack.

// by reference
const user1 = {name: 'Harsh', score: 100};
const user2 = user1;
// The user1 reference will be stored in stack memory which will point to the heap memory where these values are actually stored.
// The user2 object will be stored in stack memory which will reference to the user1 object because we assigning one object's value to the other object.
// And here, if we change the value of any one(user1/user2) object then it will reflect to the other object also because they are pointing to the same object in the heap.
```

<br />

- Always define constructor whenever you create class.

- Hoisting is JavaScript's default behavior of moving declarations to the top.
  A variable can be declared after it has been used. But always declare variable first and then use it.

<br />

### strict mode

- Defines that JavaScript code should be executed in "strict mode".
- The "use strict" directive is only recognized at the beginning of a script or a function.
- You can use strict mode in all your programs. It helps you to write cleaner code, like preventing you from using undeclared variables.

- Strict mode makes it easier to write "secure" JavaScript.
- Strict mode changes previously accepted "bad syntax" into real errors.
- In normal JavaScript, mistyping a variable name creates a new global variable. In strict mode, this will throw an error, making it impossible to accidentally create a global variable.
- In normal JavaScript, a developer will not receive any error feedback assigning values to non-writable properties.
- In strict mode, any assignment to a non-writable property, a getter-only property, a non-existing property, a non-existing variable, or a non-existing object, will throw an error.

> **Not Allowed in Strict Mode**
> Using a variable or object, without declaring it.
> Deleting variable or function.
> Duplicating a parameter name.

<br />

- Line Length < 80
  For readability, avoid lines longer than 80 characters.
- If a JavaScript statement does not fit on one line, the best place to break it, is after an operator or a comma.

<br />

- **Avoid**
  1. Global variables
  2. avoid new
  3. avoid ==
  4. avoid eval()

Accessing the HTML DOM is very slow, compared to other JavaScript statements.
