# useState

```typescript
type AuthUser = {
  name: string;
  email: string;
};

const [user, setUser] = useState<AuthUser | null>(null);

const handleLogin = () => {
  setUser({
    name: "Harsh",
    email: "harsh@gmail.com",
  });
};

const handleLogout = () => {
  setUser(null);
};

return (
  <>
    <button onClick={handleLogin}>Login</button>
    <button onClick={handleLogout}>Logout</button>
    <div>User name is: {user?.name}</div>
    <div>User email is: {user?.email}</div>
  </>
);
```

<br />

# useReducer

```typescript
type CounterState = {
  count: number;
};

type UpdateAction = {
  type: "increment" | "decrement";
  payload: number;
};

type ResetAction = {
  type: "reset";
};

type CounterAction = UpdateAction | ResetAction;

const initialState = { count: 0 };

function reducer(state: CounterState, action: CounterAction) {
  switch (action.type) {
    case "increment":
      return { count: state.count + action.payload };
    case "decrement":
      return { count: state.count - action.payload };
    case "reset":
      return initialState;
    default:
      return state;
  }
}

export const Counter = () => {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: "increment", payload: 10 })}>
        Increment 10
      </button>
      <button onClick={() => dispatch({ type: "decrement", payload: 10 })}>
        Decrement 10
      </button>
      <button onClick={() => dispatch({ type: "reset" })}>Reset</button>
    </>
  );
};
```

<br />

# useContext

```typescript
// theme.ts
export const theme = {
  primary: {
    main: "black",
    text: "white",
  },
  secondary: {
    main: "white",
    text: "black",
  },
};
```

```typescript
// ThemeContext.tsx
import React, { createContext } from "react";

type ThemeContextProviderProps = {
  children: React.ReactNode;
};

const ThemeContext = createContext(theme);

export const ThemeContextProvider = ({
  children,
}: ThemeContextProviderProps) => {
  return (
    <ThemeContext.Provider value={theme}>{children}</ThemeContext.Provider>
  );
};
```

```typescript
// Box.tsx
export const Box = () => {
  const theme = useContext(ThemeContext);
  return (
    <div
      style={{ backgroundColor: theme.primary.main, color: theme.primary.text }}
    >
      Theme context
    </div>
  );
};
```

# useContext future value

```typescript
// User.tsx
export const User = () => {
  const userContext = useContext(UserContext);
  const handleLogin = () => {
    if (userContext) {
      userContext.setUser({
        name: "Harsh",
        email: "harsh@gmail.com",
      });
    }
  };
  const handleLogout = () => {
    if (userContext) {
      userContext.setUser(null);
    }
  };
  return (
    <>
      <button onClick={handleLogin}>Login</button>
      <button onClick={handleLogout}>Logout</button>
      <div>User name is {userContext?.user?.name}</div>
      <div>User name is {userContext?.user?.email}</div>
    </>
  );
};
```

```typescript
// UserContext.tsx
import { useState, createContext } = from 'react'

export type AuthUser = {
    name: string
    email: string
}

type UserContextType = {
    user: AuthUser | null
    setUser: React.Dispatch<React.SetStateAction<AuthUser | null>>
}

type UserContextProviderProps = {
    children: React.ReactNodes
}

export const UserContext = createContext({} as UserContextType)
// in this case, there will be several changes in code because userContext will never be null
// so, userContext.user?.name
or
export const UserContext = createContext<UserContextType | null>(null)

export const UserContextProvider = ({ children }: UserContextProviderProps) => {
    const [user, setUser] = useState<AuthUser | null>(null)
    return <UserContext.Provider value={{ user, setUser }}>{children}</userContext.Provider>
}
```

<br />

# useRef

```typescript
// Example: 1
import { useRef, useEffect } from "react";

export const DomRef = () => {
  const inutRef = useRef<HTMLInputElement>(null!);
  or;
  const inutRef = useRef<HTMLInputElement>(null);

  useEffect(() => {
    inputRef.current.focus();
    or;
    inputRef.current?.focus();
  }, []);

  return (
    <>
      <input type="text" ref={inputRef} />
    </>
  );
};

// Exmaple: 2
export const MutableRef = () => {
  const [timer, setTimer] = useState(0);
  const interValRef = useRef<number | null>(null);

  const stopTimer = () => {
    if (interValRef.current) {
      window.clearInterval(interValRef.current);
    }
  };

  useEffect(() => {
    interValRef.current = window.setInterval(() => {
      setTimer((timer) => timer + 1);
    }, 1000);
    return () => {
      stopTimer();
    };
  }, []);

  return (
    <>
      HookTimer - {timer} -
      <button onClick={() => stopTimer()}>Stop Timer</button>
    </>
  );
};
```
