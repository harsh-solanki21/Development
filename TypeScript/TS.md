# Built-in Types

- number, string, boolean, null, undefined, object
- any, unknown, never, enum, tuple

# Basic Types

```typescript
let id: number = 5;
let name: string = "Harsh";
let isMarried: boolean = false;
let x: any = "Hello"; // Not a good practice to use any in TypeScript
x = 5; // no error because Data Type is set to any
```

<br />

# Casting

- Casting is the process of overriding a type.

- Casting with "as"
  A straightforward way to cast a variable is using the as keyword, which will directly change the type of the given variable.

- Casting with <>
  Using <> works the same as casting with "as".

```typescript
let x: unknown = "hello";
console.log((x as string).length); // 5

let x: unknown = "hello";
console.log((<string>x).length); // 5
```

<br />

# Arrays

```typescript
const names: string[] = ["one", "two", "three"];

const names: string[] = [];
names.push("Harsh");

// The readonly keyword can prevent arrays from being changed
const names: readonly string[] = ["Harsh"];
names.push("Jack"); // error

console.log(names[1]); // random access
```

<br />

# Tuples

- A tuple is a typed array with a pre-defined length and types for each index.

- A good practice is to make your tuple readonly.

```typescript
// Tuple
let person: [number, string, boolean] = [1, "Harsh", true];

// Tuple Array
let employee: [number, string][];
employee = [
  [1, "Harsh"],
  [2, "Nisarg"],
  [3, "Dhruva"],
];

// Example: 1
let ourTuple: [number, boolean, string];
ourTuple = [5, false, "Coding God was here"];
console.log(ourTuple);

// Example: 2
let ourTuple: [number, boolean, string];
ourTuple = [5, false, "Coding God was here"];
ourTuple.push("Something new and wrong");
console.log(ourTuple); // [ 5, false, 'Coding God was here', 'Something new and wrong' ]

// Readonly Tuple
const ourReadonlyTuple: readonly [number, boolean, string] = [
  5,
  true,
  "The Real Coding God",
];
ourReadonlyTuple.push("Coding God took a day off"); // error
```

<br />

# Union

```typescript
let pid: string | number;
pid = 22;

function kgToLbs(weight: number | string): number {
  if (typeof weight === "number") {
    return weight * 2.2;
  } else {
    return parseInt(weight) * 2.2;
  }
}

kgToLbs(10);
kgToLbs("10kg");
```

<br />

# Enum

```typescript
enum Direction1 {
  Up,
  Down,
  Left,
  Right,
}
console.log(Direction1.Up); // 0
console.log(Direction1.Down); // 1
console.log(Direction1.Left); // 2
console.log(Direction1.Right); // 3

enum Direction2 {
  Up = 1,
  Down,
  Left,
  Right,
}
console.log(Direction2.Up); // 1
console.log(Direction2.Down); // 2
console.log(Direction2.Left); // 3
console.log(Direction2.Right); // 4

enum Direction3 {
  Up = "Up",
  Down = "Down",
  Left = "Left",
  Right = "Right",
}
console.log(Direction3.Up); // Up
console.log(Direction3.Down); // Down
console.log(Direction3.Left); // Left
console.log(Direction3.Right); // Right
```

<br />

# Objects

```typescript
const user: {
  readonly id: number; // id cannot be modified
  name?: string; // optional property
  retire: (date: Date) => void;
} = {
  id: 1,
  name: "Harsh",
  retire: (date: Date) => {
    console.log(date);
  },
};

// OR

type User = {
  id: number;
  name: string;
};
const user: User = {
  id: 1,
  name: "Harsh",
};
```

<br />

# Functions

```typescript
// Optional Parameters
function add(a: number, b: number, c?: number): number {
  return a + b + (c || 0);
}

console.log(add(2, 5)); // 7

// Default Parameters
function pow(a: number, b: number = 10): number {
  return a * b;
}

console.log(pow(10)); // 100
console.log(pow(10, 20)); // 200

// Rest Parameters
function add(a: number, b: number, ...rest: number[]) {
  return a + b + rest.reduce((p, c) => p + c, 0);
}

console.log(add(10, 10, 10, 10, 10)); // 50
```

<br />

# Type Aliases

```typescript
type Employee = {
  readonly id: number;
  name: string;
  retire: (date: Date) => void;
};

const employee: Employee = {
  id: 1,
  name: "Harsh",
  retire: (date: Date) => {
    console.log(date);
  },
};
```

<br />

# Intersection Types

```typescript
type Draggable = {
  drag: () => void;
};

type Resizable = {
  resize: () => void;
};

type UIWidget = Draggable & Resizable;

let textBox: UIWidget = {
  drag: () => {},
  resize: () => {},
};
```

<br />

# Literal Types

```typescript
// Here, Literal means exact or specific
type Quantity = 50 | 100;
let quantity: Quantity = 100;

type Metric = "cm" | "inch";
let metric: Metric = "cm";
```

<br />

# Utility Types

## Partial

- Partial changes all the properties in an object to be optional.

Example:

```typescript
interface Point {
  x: number;
  y: number;
}

let pointPart: Partial<Point> = {}; // `Partial` allows x and y to be optional
pointPart.x = 10;

console.log(pointPart); // { x: 10 }
```

## Required

- Required changes all the properties in an object to be required.

```typescript
interface Car {
  make: string;
  model: string;
  mileage?: number;
}

let myCar: Required<Car> = {
  make: "Ford",
  model: "Focus",
  mileage: 12000, // `Required` forces mileage to be defined
};

console.log(myCar); // { make: 'Ford', model: 'Focus', mileage: 12000 }
```

## Record

- Record is a shortcut to defining an object type with a specific key type and value type.

```typescript
const nameAgeMap: Record<string, number> = {
  Alice: 21,
  Bob: 25,
};

console.log(nameAgeMap); // { Alice: 21, Bob: 25 }
```

## Omit

- Omit removes keys from an object type.

```typescript
interface Person {
  name: string;
  age: number;
  location?: string;
}

const bob: Omit<Person, "age" | "location"> = {
  name: "Bob",
  // `Omit` has removed age and location from the type and they can't be defined here
};

console.log(bob); // { name: 'Bob' }
```

## Pick

- Pick removes all but the specified keys from an object type.

```typescript
interface Person {
  name: string;
  age: number;
  location?: string;
}

const bob: Pick<Person, "name"> = {
  name: "Bob",
  // `Pick` has only kept name, so age and location were removed from the type and they can't be defined here
};

console.log(bob); // { name: 'Bob' }
```

## Exclude

- Exclude removes types from a union.

```typescript
type Primitive = string | number | boolean;

const value: Exclude<Primitive, string> = true;
// a string cannot be used here since Exclude removed it from the type.

console.log(typeof value); // boolean
```

## ReturnType

- ReturnType extracts the return type of a function type.

```typescript
type PointGenerator = () => { x: number; y: number };

const point: ReturnType<PointGenerator> = {
  x: 10,
  y: 20,
};
```

## Parameters

- Parameters extracts the parameter types of a function type as an array.

```typescript
type PointPrinter = (p: { x: number; y: number }) => void;

const point: Parameters<PointPrinter>[0] = {
  x: 10,
  y: 20,
};
```

<br />

# Optional Chaining

```typescript
type Customer = {
  birthday?: Date;
};

function getCustomer(id: number): Customer | null | undefined {
  return id === 0 ? null : { birthday: new Date() };
}

let customer = getCustomer(0);
console.log(customer?.birthday?.getFullYear()); // optional property access operator

// Optional element access operator
customer?.[0];

// Optional call
let log: any = null;
log?.("a");
```

<br />

# Interface

- Interfaces are similar to type aliases, except they only apply to object types.

- Interfaces can extend each other's definition.
- Extending an interface means you are creating a new interface with the same properties as the original, plus something new.

```typescript
// Eg.1
interface UserInterface {
  readonly id: number; // readonly field (cannot reassign value)
  name: string;
  age?: number; // optional field
}
const user: UserInterface = {
  id: 1,
  name: "Harsh",
};
console.log(user); // { id: 1, name: "Harsh" }

// Eg.2
interface MathFunc {
  (x: number, y: number): number; // function
}
const add: MathFunc = (x: number, y: number): number => x + y;

// Extending Interfaces
interface Rectangle {
  height: number;
  width: number;
}

interface ColoredRectangle extends Rectangle {
  color: string;
}

const coloredRectangle: ColoredRectangle = {
  height: 20,
  width: 10,
  color: "red",
};

console.log(coloredRectangle); // { height: 20, width: 10, color: 'red' }
```

<br />

# Classes

```typescript
class Person {
  private id: number;
  name: string;

  constructor(id: number, name: string) {
    this.id = id;
    this.name = name;
  }
}
const harsh = new Person(1, "Harsh");
```

<br />

# Generics

- Generics makes it easier to write reusable code.

```typescript
// Eg.1
function getArray<T>(items: T[]): T[] {
  return new Array().concat(items);
}

let numArrays = getArray<number>([1, 2, 3]);
let numArrays = getArray<string>(["one", "two", "three"]);

// Eg.2
function createPair<S, T>(v1: S, v2: T): [S, T] {
  return [v1, v2];
}

console.log(createPair<string, number>("hello", 42)); // ['hello', 42]

// Type Aliases
type Wrapped<T> = { value: T };
const wrappedValue: Wrapped<number> = { value: 10 };
```

# Null

## Optional Chaining

- It allows accessing properties on an object, that may or may not exist, with a compact syntax. It can be used with the ?. operator when accessing properties.

Example:

```typescript
interface House {
  sqft: number;
  yard?: {
    sqft: number;
  };
}

function printYardSize(house: House) {
  const yardSize = house.yard?.sqft;

  if (yardSize === undefined) {
    console.log("No yard");
  } else {
    console.log(`Yard is ${yardSize} sqft`);
  }
}

let home: House = {
  sqft: 500,
};

printYardSize(home); // 'No yard'
```

## Nullish Coalescence

- It allows writing expressions that have a fallback specifically when dealing with null or undefined. This is useful when other falsy values can occur in the expression but are still valid. It can be used with the ?? operator in an expression, similar to using the && operator.

```typescript
function printMileage(mileage: number | null | undefined) {
  console.log(`Mileage: ${mileage ?? "Not Available"}`);
}

printMileage(null); // 'Mileage: Not Available'
printMileage(undefined); // 'Mileage: Not Available'
printMileage(0); // 'Mileage: 0'
```
