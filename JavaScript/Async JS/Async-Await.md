# Async / Await

## Async

- We use the `async` keyword before a function to represent that the function is an asynchronous function. The async function returns a promise.

```javascript
// async function example
async function fun() {
  console.log("Async function");
  return Promise.resolve(1);
}

fun();
```

<br />

- Since the function returns a promise, you can use the chaining method then() like this:

```javascript
async function f() {
  console.log("Async function.");
  return Promise.resolve(1);
}

f().then(function (result) {
  console.log(result);
});
```

<br />

## Await

- The `await` keyword can only be used inside an `async` function to wait for the asynchronous operation.

- The syntax to use await is:
  `let result = await promise;`

- The use of await pauses the async function until the promise returns a result (resolve or reject) value. For example,

```javascript
// async function
async function asyncFunc() {
  // wait until the promise resolves
  const result = await promise;
  console.log(result);
  console.log("hello");
}

// calling the async function
asyncFunc();
```

**_Note: You can use await only inside of async functions._**

<br />

## Error Handling

While using the async function, you write the code in a synchronous manner. And you can also use the catch() method to catch the error.

```javascript
asyncFunc()
  .catch
  // catch error and do something
  ();

// Other way to handle an error is by using `try/catch` block.
async function asyncFunc() {
  try {
    const result = await promise;
    console.log(result);
  } catch (error) {
    console.log(error);
  }
}

asyncFunc(); // Promise resolved
```

## Pros of using `Async` function:

1. The code is more readable than using a callback or a promise.
2. Error handling is simpler.
3. Debugging is easier.
