# Debouncing & Throttling

## Debouncing

- It's a technique that delays the execution of a function until a certain amount of time has passed since the last time it was called.
- It's used to prevent excessive or unnecessary function calls, especially in response to frequent events like keystrokes, resize events, or scroll events.
- This optimization improves performance and user experience by reducing the number of times a function is executed.

#### How it Works:

1. **Initial Call:** When a function is debounced, it's wrapped in a debounce function.
2. **Timer:** The debounce function starts a timer with a specified delay.
3. **Subsequent Calls:** If the function is called again before the timer expires, the timer is reset.
4. **Execution:** Once the timer expires without any further calls, the original function is finally executed.

#### Example:

```javascript
function debounce(func, delay) {
  let timer;
  return function () {
    clearTimeout(timer);
    timer = setTimeout(() => {
      func.apply(this, arguments);
    }, delay);
  };
}

const searchInput = document.getElementById("search");
const debouncedSearch = debounce(fetchSearchResults, 500); // Delay of 500 milliseconds

searchInput.addEventListener("input", debouncedSearch);
```

<br />

#### Pros:

- **Performance Optimization:** Reduces unnecessary function calls, saving CPU cycles and improving responsiveness.
- **Enhanced User Experience:** Prevents unintended actions or overwhelming the user with too many updates.
- **API Call Management:** Reduces the number of API calls, saving server resources and bandwidth.

#### Common Use Cases:

- **Search box suggestions:** Delaying API calls until the user pauses typing.
- **Text field auto-saves:** Saving data only after a pause in typing.
- **Window resize events:** Optimizing layout adjustments.
- **Scroll events:** Throttle expensive updates during scrolling.
- **Button double-click prevention:** Ensuring only one click is registered.

#### Key Points:

- Debouncing delays execution until a period of inactivity.
- It's ideal for handling events that fire frequently.
- Customize the delay time for different use cases.
- Consider using built-in debounce functions from libraries like Lodash or Underscore.js.

**PS - Debouncing: Delay execution until inactivity.**

<br />

## Throttling

- It's a technique that limits the rate at which a function can be called within a given time interval.
- It ensures that the function doesn't execute more often than a specified maximum number of times per interval.
- It's used to optimize performance and prevent overwhelming systems or APIs with too many requests.

#### How it Works:

1. **First Call:** The first time the throttled function is invoked, it executes immediately.
2. **Timer:** A timer is set with the specified interval.
3. **Subsequent Calls:** If the function is called again within the interval, it's delayed until the timer expires.
4. **Execution:** Once the timer expires, the function is allowed to execute again, and the timer is reset.

#### Example:

```javascript
function throttle(func, delay) {
  let waiting = false;
  return function () {
    if (!waiting) {
      func.apply(this, arguments);
      waiting = true;
      setTimeout(() => {
        waiting = false;
      }, delay);
    }
  };
}

const scrollContainer = document.getElementById("container");
const throttledScrollHandler = throttle(handleScroll, 250); // Throttle to 250 milliseconds

scrollContainer.addEventListener("scroll", throttledScrollHandler);
```

<br />

#### Pros:

- **Performance Optimization:** Prevents excessive function calls and potential performance bottlenecks.
- **API Rate Limiting:** Ensures your application adheres to API rate limits and avoids overwhelming servers.
- **Improved User Experience:** Prevents UI hiccups or delays caused by too many actions in a short time.
- **Resource Management:** Conserves resources like CPU, memory, and network bandwidth.

#### Common Use Cases:

- **Window resize events:** Throttle expensive layout calculations.
- **Mouse move events:** Throttle updates to avoid overwhelming the browser.
- **Scroll events:** Throttle heavy updates or API calls during scrolling.
- **API calls with rate limits:** Enforce rate limits to prevent errors.
- **Real-time updates:** Manage the frequency of updates to avoid overwhelming the user.

#### Key Points:

- Throttling limits the function execution rate to a maximum frequency.
- It's ideal for handling events that fire rapidly but don't require immediate responses.
- Adjust the throttling interval based on your specific use case and performance goals.
- Consider using built-in throttle functions from libraries like Lodash or Underscore.js.

**PS - Throttling: Limit execution rate to a maximum frequency.**
