# Template Literals and Exclude

```typescript
// Toast.tsx
type HorizontalPosition = "left" | "center" | "right";
type VerticalPosition = "top" | "center" | "bottom";

type ToastProps = {
  position:
    | Exclude<`${HorizontalPosition}-${VerticalPosition}`, "center-center">
    | "center";
  // center-center will be excluded
};

export const Toast = ({ position }: ToastProps) => {
  return <div>Toast notification position = {position}</div>;
};
```

```typescript
// App.tsx
<Toast position="left-center" />
```

<br />

# Wrapping HTML Elements

```typescript
// CustomButton.tsx
type ButtonProps = {
  variant: "primary" | "secondary";
  children: string;
} & Omit<React.ComponentProps<"button">, "children">;

export const CustomButton = ({ variant, children, ...rest }: ButtonProps) => {
  return (
    <button className={`class-with-${variant}`} {...rest}>
      {children}
    </button>
  );
};
```

```typescript
// CustomInput.tsx
type InputProps = React.ComponentProps<"input">;

export const CustomInput = (props: InputProps) => {
  return <input {...props} />;
};
```

```typescript
// App.tsx
<CustomButton variant="primary" onClick={() => console.log("clicked")}>
  Primary Button // It won't accept <div>Primary Button</div> because of omit
</CustomButton>
```

<br />

# Extracting component's prop types

```typescript
// When we want to extract other component's type
// Suppose we want to extract Greet component's type

import { Greet } from "../Greet";

export const CustomComponent = (props: React.ComponentProps<typeof Greet>) => {
  return <div>{props.name}</div>;
};
```

<br />

# Polymorphic Components

```typescript
// Text.tsx
type TextOwnProps<E extends React.ElementType> = {
  size?: "sm" | "md" | "lg";
  color?: "primary" | "secondary";
  children: React.ReactNode;
  as?: E; // string will give error as any random string cannot be HTML element
};

type TextProps<E extends React.ElementType> = TextOwnProps<E> &
  Omit<React.ComponentProps<E>, keyof TextOwnProps<E>>;

export const Text = <E extends React.ElementType = "div">({
  size,
  color,
  children,
  as,
}: TextProps<E>) => {
  const Component = as || "div";
  return (
    <Component className={`class-with-${size}-${color}`}>{children}</Component>
  );
};
```

```typescript
// App.tsx
<Text as='h1' size='lg'>Heading</Text>
<Text as='p' size='md'>Paragraph</Text>
<Text as='label' htmlFor='someId' size='sm' color='secondary'>Label</Text>
```
