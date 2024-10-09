# Go Routines, Mutex, Channels, Wait Groups, Select

## Goroutines

- Goroutines is a lightweight, independently running function that allows concurrent execution in a program. It's like a mini-thread managed by the Go runtime, making it easy to run multiple tasks simultaneously.
- Goroutines are a key feature for concurrent programming in the Go language.

```go
func sendMsg(msg string) {
	time.Sleep(time.Duration(rand.Intn(1000)) * time.Millisecond)
	fmt.Println(msg)
}

func main() {
	sendMsg("hello") // sync

	go sendMsg("test1") // async
	go sendMsg("test2") // async
	go sendMsg("test3") // async

	sendMsg("main") // sync

	time.Sleep(2 * time.Second)
}
```

- When the sendMsg function is called with the go keyword, the main function will not wait for the sendMsg function to finish executing before it continues to the next line of code and will return immediately after the sendMsg function is called.

- Otherwise, the function is called synchronously, and the main function will wait for the sendMsg function to finish executing before it continues to the next line of code.

<br />

## Mutex

- Mutex is a synchronization mechanism that allows only one goroutine to access a shared resource at a time. It's like a lock that ensures that only one goroutine can modify the shared resource at a time.

**Example:**

```go
func worker(wg *sync.WaitGroup, mutex *sync.Mutex, counter *int) {
    mutex.Lock()
    *counter++
    mutex.Unlock()
    wg.Done()
}

func main() {
    var w sync.WaitGroup
    var m sync.Mutex
    counter := 0

    for i := 0; i < 1000; i++ {
        w.Add(1)
        go worker(&w, &m, &counter)
    }

    w.Wait()
    fmt.Println("Value of x", counter)
}
```

<br />

## Channels

- Channels are the medium through which goroutines can communicate with each other. In simple terms, a channel is a pipe that allows a goroutine to either put or read the data.

**Example:**

```go
func sendData(ch chan<- int) {
    ch <- 20
}

func main() {
    ch := make(chan int)
    go sendData(ch)
    value := <- ch
    fmt.Println("Received: ", value)
}
```

#### Types of Channels

**1. Unbuffered Channels**

- An unbuffered channel has a capacity of 0.
- Each send operation on an unbuffered channel block until there is a corresponding receive operation, and vice versa.
- This creates a direct, synchronous communication between the sender and the receiver.

**2. Buffered Channels**

- A buffered channel has a specified capacity greater than 0.
- It allows multiple values to be sent into the channel without an immediate corresponding receiver.
- Send operaitons on a buffered channel block only when the buffer is full, and receive operaitons block only when the buffer is empty.

**Example:**

```go
func main() {
    // Unbuffered channel
    unbufferedCh := make(chan int)

    // Buffered channel
    bufferedCh := make(chan string, 2)

    go func() {
        unbufferedCh <- 20
    }()

    go func() {
        bufferedCh <- "Hello"
        bufferedCh <- "World"
        close(bufferedCh)
    }()

    value := <- unbufferedCh
    fmt.Println("Received from unbuffered channel: ", value)

    fmt.Println("Received from buffered channel: ")
    for msg := range bufferedCh {
        fmt.Println(msg)
    }
}
```

<br />

## Wait Groups

- WaitGroups are used to wait for a collection of goroutines to finish executing.
- It allows you to synchronize the main goroutine with a group of worker goroutines.

**Example:**

```go

func printMessage(wg *sync.WaitGroup, msg string) {
    defer wg.Done()  // Decrement the WaitGroup counter when the goroutine completes
    fmt.Println(msg)
    time.Sleep(time.Second)
}

func main() {
    var wg sync.WaitGroup
    wg.Add(3) // Set the number of goroutines to wait for

    go printMessage(&wg, "Hello")
    go printMessage(&wg, "Go")
    go printMessage(&wg, "Wait Group")

    wg.Wait() // Wait for all goroutines to finish
    fmt.Println("All goroutines have finished.")
}
```

<br />

## Select

- The Select statement is used to handle multiple channels in a non-blocking manner. It provides a way to wait on multiple communication operations simultaneously and executes the first case that is ready.

**Example:**

```go
func main() {
	c1 := make(chan string)
	c2 := make(chan string)

	go func() {
		time.Sleep(1 * time.Second)
		c1 <- "one"
	}()
	go func() {
		time.Sleep(2 * time.Second)
		c2 <- "two"
	}()

	for i := 0; i < 2; i++ {
		select {
		case msg1 := <-c1:
			fmt.Println("received", msg1)
		case msg2 := <-c2:
			fmt.Println("received", msg2)
		}
	}
}
```
