# Promise

### What is Promise?

- Promises are objects that represent the eventual outcome of an asynchronous operation.
- Also used to avoid callback hell.

<br />

**A Promise object can be in one of three states:**

- **Pending:** The initial state, the operation has not completed yet.
- **Fulfilled:** The operation has completed successfully and the promise now has a resolved value.
- **Rejected:** The operation has failed and the promise has a reason for the failure. This reason is usually an Error of some kind.

<br />

### Constructing a Promise Object

```javascript
const executorFunction = (resolve, reject) => {};
const myFirstPromise = new Promise(executorFunction);
```

<br />

- The executor function has two function parameters, usually referred to as the resolve() and reject() functions. The resolve() and reject() functions aren’t defined by the programmer. When the Promise constructor runs, JavaScript will pass its own resolve() and reject() functions into the executor function.

- `resolve` is a function with one argument. Under the hood, if invoked, resolve() will change the promise’s status from pending to fulfilled, and the promise’s resolved value will be set to the argument passed into resolve().
- `reject` is a function that takes a reason or error as an argument. Under the hood, if invoked, reject() will change the promise’s status from pending to rejected, and the promise’s rejection reason will be set to the argument passed into reject().

<br />

```javascript
// Example executor function in a Promise constructor:
const executorFunction = (resolve, reject) => {
  if (someCondition) {
    resolve("I resolved!");
  } else {
    reject("I rejected!");
  }
};

const myFirstPromise = new Promise(executorFunction);
```

<br />

### Promise Chaining

- Promises are useful when you have to handle more than one asynchronous task, one after another. For that, we use promise chaining.
- You can perform an operation after a promise is resolved using methods `then()`, `catch()` and `finally()`.
- `then()` method is used with the callback when the promise is resolved successfully.
- `catch()` method is used with the callback when the promise is rejected or if an error occurs.
- `finally()` method gets executed when the promise is either resolved successfully or rejected.

```javascript
function fetchUserData(userId) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (userId === 123) {
        resolve({ id: userId, name: "John Doe" });
      } else {
        reject(new Error("User not found"));
      }
    }, 1000);
  });
}

function fetchUserPosts(user) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve([
        { id: 1, title: "Post 1" },
        { id: 2, title: "Post 2" },
      ]);
    }, 1000);
  });
}

function displayUserInfo(user, posts) {
  console.log(`User: ${user.name}`);
  console.log("Posts:");
  posts.forEach((post) => console.log(`- ${post.title}`));
}

let timer;

fetchUserData(123)
  .then((user) => {
    console.log("User data fetched");
    return fetchUserPosts(user);
  })
  .then((posts) => {
    console.log("User posts fetched");
    return { user: { id: 123, name: "John Doe" }, posts };
  })
  .then(({ user, posts }) => {
    displayUserInfo(user, posts);
  })
  .catch((error) => {
    console.error("An error occurred:", error);
  })
  .finally(() => {
    console.log("Operation completed");
    clearTimeout(timer);
  });

// Start a timer
timer = setTimeout(() => {
  console.log("Operation timed out");
}, 5000);
```

<br />

### Promise.all()

- The JavaScript `Promise.all()` method can be used to execute multiple promises in `parallel`.
- The function accepts an array of promises as an argument. If all of the promises in the argument are resolved, the promise returned from Promise.all() will resolve to an array containing the resolved values of all the promises in the order of the initial array.
- Any rejection from the list of promises will cause the greater promise to be rejected.

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(3);
  }, 300);
});
const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(2);
  }, 200);
});

Promise.all([promise1, promise2]).then((res) => {
  console.log(res[0]);
  console.log(res[1]);
});
```

<br />

### When a promise in Promise.all() Fails

1. Promise.all() immediately rejects with the reason of the first promise that rejects.
2. The previously resolved promises do not get reverted. Their results are simply discarded.
3. Any pending promises continue to execute, but their results are ignored.

<br />

- It's important to note that Promise.all() follows a `fail-fast` behavior. As soon as one promise rejects, the entire Promise.all() rejects, regardless of the state of other promises.
- The resolved promises `don't revert` because promises are designed to be `immutable` once settled. Once a promise is fulfilled or rejected, its state and value cannot change.
- If you need all promises to complete regardless of their individual outcomes, you might consider using `Promise.allSettled()` instead. This method waits for all promises to settle (either fulfill or reject) and returns an array of objects describing the outcome of each promise.

**Example**

```javascript
const promise1 = Promise.resolve(3);
const promise2 = new Promise((resolve, reject) =>
  setTimeout(reject, 100, "foo")
);
const promise3 = new Promise((resolve) => setTimeout(resolve, 200, "bar"));
const promise4 = Promise.reject("baz");

Promise.allSettled([promise1, promise2, promise3, promise4]).then((results) => {
  results.forEach((result, index) => {
    if (result.status === "fulfilled") {
      console.log(`Promise ${index + 1} fulfilled with value:`, result.value);
    } else if (result.status === "rejected") {
      console.log(`Promise ${index + 1} rejected with reason:`, result.reason);
    }
  });
});

// Output:
// Promise 1 fulfilled with value: 3
// Promise 2 rejected with reason: foo
// Promise 3 fulfilled with value: bar
// Promise 4 rejected with reason: baz
```

<br />

- If you need to revert or cancel all previously resolved promises when any promise fails in Promise.all() then consider using `Transaction`.
