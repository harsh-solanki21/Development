# Redux Toolkit and React-Redux

Redux Toolkit serves as an abstraction over Redux. It is a library for efficient Redux development.

React-Redux is the official Redux UI binding library for React.

## @reduxjs/toolkit react-redux

This package consists of a few libraries:

- redux (core library, state management)
- immer (allows to mutate state)
- redux-thunk (handles async actions)
- reselect (simplifies reducer functions)

## Reducers and Extrareducers

### Reducers

The `reducers` property both creates an action creator function and responds to that action in the slice reducer. You will use reducers most of the time.

### Extrareducers

The `extraReducers` allows you to respond to an action in your slice reducer but does not create an action creator function.

You would use `extraReducers` when you are dealing with an action that you have already defined somewhere else. The most common examples are:

1. Responding to a `createAsyncThunk` action
2. Responding to an action from another slice
