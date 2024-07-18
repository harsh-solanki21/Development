# Props

#### Example:

```typescript
// Greet.tsx
type GreetProps = {
  name: string;
  messageCount?: number; // ? shows optional props
  isLoggedIn: boolean;
  fullName: {
    // object
    first: string;
    last: string;
  };
  names: {
    // array
    first: string;
    last: string;
  }[];
};

export const Greet = (props: GreetProps) => {
  const { messageCount = 0 } = props;
  // if props are not passed then it will take 0 as default messageCount

  return (
    <>
      <h2>
        {props.isLoggedIn
          ? `Welcome {props.name}! You have {messageCount} unread messages.`
          : `Welcome Guest`}
      </h2>
      <div>
        {props.names.map((name) => {
          return (
            <h2 key={name.first}>
              {name.first} {name.last}
            </h2>
          );
        })}
      </div>
    </>
  );
};
```

```typescript
// App.tsx
function App() {
    const fullName = { first: 'Harsh', last: 'Solanki' }
    const names = [
        { first: 'Harsh', last: 'Solanki' },
        { first: 'Nisarg', last: 'Dodiya' }
    ]
    <Greet name='Harsh' messageCount={10} isLoggedIn={false} fullName={fullName} names={names}/>
}
```

<br />

## Advanced Props

```typescript
// Status.tsx
type StatusProps = {
  status: "loading" | "success" | "error";
};

export const Status = (props: StatusProps) => {
  let message;
  if (props.status === "loading") {
    message = "Loading...";
  } else if (props.status === "success") {
    message = "Data fetched successfully!";
  } else if (props.status === "error") {
    message = "Error fetching data";
  }

  return (
    <>
      <h2>Status - {message}</h2>
    </>
  );
};
```

```typescript
// Heading.tsx
type HeadingProps = {
  children: string;
};

export const Heading = (props: HeadingProps) => {
  return <h2>{props.children}</h2>;
};
```

```typescript
// App.tsx
function App() {
    <Greet status='loading' />
    <Heading>Placeholder text</Heading>
}
```

<br />

## Event Props

```typescript
// Button.tsx
type ButtonProps = {
  handleClick: () => void;
  handleClick2: (event: React.MouseEvent<HTMLButtonElement>) => void;
  handleClick3: (
    event: React.MouseEvent<HTMLButtonElement>,
    id: number
  ) => void;
};

export const Button = (props: ButtonProps) => {
  return (
    <>
      <button onClick={props.handleClick}>Click</button>
      <button onClick={(event) => props.handleClick(event, 1)}>Click</button>
    </>
  );
};
```

```typescript
// Input.tsx
type InputProps = {
  value: string;
  handleChange: (event: React.ChangeEvent<HTMLInputElement>) => void;
};

export const Input = ({ value, handleChange }: InputProps) => {
  const handleInputChange = (event: React.ChangeEvent<HTMLInputElement>) => {
    console.log(event);
  };
  return <input type="text" value={value} onChange={handleChange} />;
};
```

```typescript
// App.tsx
function App() {
  return (
    <>
      <Button
        handleClick={() => {
          console.log("Button clicked");
        }}
      />
      <Button
        handleClick2={(event) => {
          console.log("Button clicked", event);
        }}
      />
      <Button
        handleClick3={(event, id) => {
          console.log("Button clicked", event, id);
        }}
      />

      <Input value="" handleChange={(event) => console.log(event)} />
    </>
  );
}
```

<br />

## Style Props

```typescript
// Container.tsx
type ContainerProps = {
  styles: React.CSSProperties;
};

export const Container = (props: ContainerProps) => {
  return <div style={props.styles}>Text content goes here</div>;
};
```

```typescript
// App.tsx
function App() {
  <Container styles={{ border: "1px solid black", padding: "1rem" }} />;
}
```

<br />

## Component Prop

```typescript
// Login.tsx
export const Login = () => {
  return <div>Please login to continue</div>;
};
```

```typescript
// Profile.tsx
export type ProfileProps = {
  name: string;
};

export const Profile = ({ name }: ProfileProps) => {
  return <div>Private profile component. Name is {name}</div>;
};
```

```typescript
// Private.tsx
type PrivateProps = {
  isLoggedIn: boolean;
  component: React.ComponentType<ProfileProps>;
};

export const Private = ({ isLoggedIn, component: Component }: PrivateProps) => {
  if (isLoggedIn) {
    return <Component name="Harsh" />;
  } else {
    return <Login />;
  }
};
```

```typescript
// App.tsx
<Private isLoggedIn={true} component={Profile} />
```

<br />

## Generic Props

```typescript
// List.tsx
type ListProps<T> = {
    items: T[]
    onClick: (value: T) => void
}

export const List = <T extends {}>({ items, onClick }: ListProps<T>) => {
    // <T extends string | number>
    // In case of Array of object -> <T extends { id: number }>
    return (
        <>
            <h2>List of items</h2>
            {items.map((item, index) => {
                return (
                    <div key={index} onClick={() => onClick(item)}>
                        // In case of Array of object -> key={ item.id }
                        { item }
                    </div>
                )
            })}
        </>
    )
}
```

```typescript
// App.tsx
<List items={['Batman', 'Superman', 'Ironman']} onClick={(item) => console.log(item)} />
<List items={[1, 2, 3]} onClick={(item) => console.log(item)} />
<List items={[
    { id: 1, first: 'Bruce', last: 'Wayne' },
    { id: 2, first: 'Clark', last: 'Kent' },
    { id: 3, first: 'Tony', last: 'Stark' }
]} onClick={(item) => console.log(item)} />
```

<br />

## Restricting Props

```typescript
// RandomNumber.tsx
type RandomNumberType = {
  value: number;
};

type PositiveNumber = RandomNumberType & {
  isPositive: boolean;
  isNegative?: never;
  isZero?: never;
};

type NegativeNumber = RandomNumberType & {
  isNegative: boolean;
  isPositive?: never;
  isZero?: never;
};

type Zero = RandomNumberType & {
  isZero: boolean;
  isPositive?: never;
  isNegative?: never;
};

type RandomNumberProps = PositiveNumber | NegativeNumber | Zero;

export const RandomNumber = ({
  value,
  isPositive,
  isNegative,
  isZero,
}: RandomNumberProps) => {
  return (
    <>
      {value} {isPositive && "positive"} {isNegative && "negative"}{" "}
      {isZero && "zero"}
    </>
  );
};
```

```typescript
// App.tsx
<RandomNumber value={10} isPositive /> // isPositive is true by default
```

<br />

> When we work with large components with multiple types, we should make a separate file for it. Make type declaration file with .d.ts extension.
