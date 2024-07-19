# Variables

### var

- If you use var outside of a function, it belongs to the global scope.
- If you use var inside of a function, it belongs to that function.
- If you use var inside of a block, i.e. a for loop, the variable is still available outside of that block.

### let

- let is the block scoped version of var, and is limited to the block (or expression) where it is defined.
- If you use let inside of a block, i.e. a for loop, the variable is only available inside of that loop.

### const

- const is a variable that once it has been created, its value can never change.
- const has a block scope.
