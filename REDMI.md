## React Redux

###### React Redux is the Official React Ul Bindings layer for Redux. It lets your React componets read data from a Redux store and Dispathc actions to the store to update state.

## Create a React Redux App

###### To use React Redux with your React app, install it as a dependency:

#### IF you use npm

```javascript
npm install --save react-redux
```

##### Following is a diagram which shows how the data actually flows through all the above-described components in Redux.

![My animated logo](./flowda.png)

##### Install Redux Toolkit and react redux

```javascript
npm install @reduxjs/toolkit react-redux
```

## React Redux Components Provider

react redux includs a "Provider" components which makes the redux store available to the rest of your app

##### create a redux store

<p>create a file name src/app/store.js. Import the configurStore Api from Redux Toolkit. We"ll start by creating an empty Redux store, and exporiting it
</p>

app/store.js

```javascript
import { configureStore } from "@reduxjs/toolkit";

export default configureStore({
  reducer: {},
});
```

##### Provide the Redux Store to React

```javascript
import { Provider } from "react-redux";
import store from "./js/store/index";
//Must be imported from React Reader

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);
```

As you can see Provider wraps up your React application and makes it aware of the entire Redux's store.

###### Create a Redux State Slice

<span style="color:red">
Folder 
</span>

features/counter/counterSlice.js

```javascript
import { createSlice } from "@reduxjs/toolkit";

export const counterSlice = createSlice({
  name: "counter",
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;
export default counterSlice.reducer;
```

##### Add Slice Reducres to the Store

```javascript
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "../features/counter/counterSlice";

export default configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

##### Use Redux State and Actions in React Components

```javascript
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { decrement, increment } from "./counterSlice";
import styles from "./Counter.module.css";

export function Counter() {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      <div>
        <button
          aria-label="Increment value"
          onClick={() => dispatch(increment())}
        >
          Increment
        </button>
        <span>{count}</span>
        <button
          aria-label="Decrement value"
          onClick={() => dispatch(decrement())}
        >
          Decrement
        </button>
      </div>
    </div>
  );
}
```
