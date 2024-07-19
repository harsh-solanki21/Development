# Redux

## Overview

- When a JavaScript application grows big, it becomes difficult for the user to manage its state.
- Redux solves this problem by managing application's state with a single global object called Store.
- It makes testing easy.
- Provides consistency throughout the application.

## Redux Flow

Action → Reducer → Store → UI → Action

<br />

## Components

### Action

- An Action is a plain object that describes the intention to cause change with a type property.
- The type property tells what type of action is being performed.
- Actions only tell what to do, but they don't tell how to do.
- Actions have 2 properties:
  1. type: which is a unique identifier
  2. payload: which has data

### Reducer

- A Reducer is the function that determines changes to the state and returns the newly updated state.

### Store

- A Store brings together the state, actions and reducers that make up the app.
- Redux provides a single store that you can use to manage a large amount of data.
- Multiple stores are possible but it is not recommended.

<br />

## Pros of Redux

- It makes state changes predictable and transparent
- It centralizes our application state (so all the data that application needs is stored in a single place that is accessible by all parts of the UI)
- Easy debugging
- Easily cache/preserve page state
- Implement undo/redo features

## When Not to Use Redux

- Tight budget
- Small to medium-size apps
- Simple UI/data flow
- Static data

<br />

## Example

### Action Creator

```jsx
export const depositMoney = (amount) => {
  return (dispatch) => {
    dispatch({
      type: "deposit",
      payload: amount,
    });
  };
};

export const withdrawMoney = (amount) => {
  return (dispatch) => {
    dispatch({
      type: "withdraw",
      payload: amount,
    });
  };
};
```

### Reducer

```jsx
export default reducer = (state = 0, action) => {
  // if the value for state has passed then that value will be taken otherwise it will take by default value 0
  if (action.type === "deposit") {
    return state + action.payload;
  } else if (action.type === "withdraw") {
    return state - action.payload;
  } else {
    return state;
  }
};
```
