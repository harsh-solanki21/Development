# Go Contexts

- Context provides a mechanism to control the lifecycle, cancellation, and propagation of requests across multiple goroutines.
- A Context carries a cancellation signal and request-scoped values to all functions running on behalf of the same task. It's safe for concurrent access.

<br />

### Problems without Context

- Assume you start a function and need to send some common parameters to the remaining functions. You cannot give these common parameters as arguments to all downstream functions.
- For solving this, You created a goroutine, which in turn activated more goroutines, and so on. Imagine the task you were working on is no longer required. Then, how should all child goroutines be informed to gently terminate so that resources can be freed up?
- A task should be executed within a time limit, say 3 seconds. Otherwise, it should gently stop or return.
- A task should be completed by a specific deadline, such as per the specific time provided. If it is not completed, it should peacefully stop and return.

<br />

### Context Types

1. `context.Background()`: Returns an empty context; It is usually used as the root context for the entire application.
2. `context.TODO()`: Returns a context that can be used when a context is required but not yet defined; It signals that the context needs further work.
3. `context.WithCancel(parent Context)`: Returns a derived context that can be canceled by calling the cancel function
4. `context.WithDeadline(parent Context, d time.Time)`: Returns a derived context that automatically cancels at a specified time (deadline)
5. `context.WithTimeout(parent Context, timeout time.Duration)`: Similar to the WithDeadline, but the deadline is set by a duration
6. `context.WithValue(parent Context, key, val interface{})`: Returns a derived context that contains a key-value pair

### Context Types Example

```go
func main() {
    // Context with Background
    ctx := context.Background()

    // Context with Todo
    ctx := context.TODO()

	// Context with cancellation
    // A context with cancelation is useful when you need to stop a goroutine based on an event.
	ctx, cancel := context.WithCancel(context.Background())
	defer cancel()

    // Context with deadline
    ctx, cancel := context.WithDeadline(context.Background(), time.Now().Add(5*time.Second))
    defer cancel()

    // Context with timeout
    ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
	defer cancel()

    // Context with values
    ctx := context.WithValue(context.Background(), key("user"), "harsh")
}
```

### Best Practices

1. Always pass context as the first parameter to functions that may perform long-running operations
2. Use context.TODO() if you're unsure about which context to use
3. Don't store contexts in structs; pass them explicitly
4. The context should flow through your program from top to bottom
5. Use context values only for request-scoped data, not for passing optional parameters
