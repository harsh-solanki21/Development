# new() and make() Keywords

## new()

- allocates memory, but does not initialize it
- returns a pointer to the memory
- zero valued (IMP)

## make()

- allocates memory, also initialize it
- returns a pointer to the memory
- non-zero valued (IMP)

### Example

```go
type Person struct {
    Name string
    Age int
}

func main() {
    a := new(Person);
    fmt.Println(*a);  // { 0 }
    // zero valued, returns pointer

    friends := make(map[string]int);
    fmt.Println(friends); // map[]
    // non-zero valued, returns pointer
}
```

> Using make() is best practice.
