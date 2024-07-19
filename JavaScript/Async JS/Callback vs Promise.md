# Callbacks VS Promises

- Promises are similar to callback functions in a sense that they both can be used to handle asynchronous tasks.

## Promises

1. The syntax is user-friendly and easy to read.
2. Error handling is easier to manage.

**Example:**

```javascript
api()
  .then(function (result) {
    return api2();
  })
  .then(function (result2) {
    return api3();
  })
  .then(function (result3) {
    // do work
  })
  .catch(function (error) {
    // handle any error that may occur before this point
  });
```

<br />

## Callback (Callback Hell)

1. The syntax is difficult to understand.
2. Error handling may be hard to manage.

**Example:**

```javascript
api(function (result) {
  api2(function (result2) {
    api3(function (result3) {
      // do work
      if (error) {
        // do something
      } else {
        // do something
      }
    });
  });
});
```
