# React Concepts

## Redux

### What
A state management library for JavaScript applications.

### Why
- Helps manage global state by providing a single source of truth.
- Makes it easier to debug and test applications.
- Enhances scalability and maintainability.

### Core Concepts
- **Store:** The central location of the application's state.
- **Actions:** Payloads that trigger state changes.
- **Reducers:** Pure functions that update the state based on actions.
- **Dispatch:** Sends actions to the store to update the state.

### Where
#### Scenario
A simple counter application with increment and decrement buttons.

#### Use Case
Use Redux to manage the counter state and update it based on user interactions.

#### Code Snippet
```jsx
// src/redux/store.js

import { createStore } from 'redux';

const initialState = { count: 0 };

const counterReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
};

const store = createStore(counterReducer);

export default store;

// src/redux/actions.js

export const increment = () => ({ type: 'INCREMENT' });
export const decrement = () => ({ type: 'DECREMENT' });

// src/components/Counter.js

import React from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { increment, decrement } from '../redux/actions';

const Counter = () => {
  const count = useSelector(state => state.count);
  const dispatch = useDispatch();

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => dispatch(increment())}>Increment</button>
      <button onClick={() => dispatch(decrement())}>Decrement</button>
    </div>
  );
};

export default Counter;
```

---

## Middleware

### What
Software that connects and facilitates communication between different applications, services, or systems.

### Why
- Enables communication and data exchange between disparate systems.
- Provides a layer of abstraction for easier integration and scalability.
- Enhances security, logging, and error handling.

### Types
- **Request middleware:** Executes before the request reaches the application.
- **Response middleware:** Executes after the response leaves the application.
- **Error middleware:** Handles errors and exceptions.

### Where
#### Scenario
Logging incoming requests and responses in an Express.js application.

#### Use Case
Use middleware to log requests and responses.

#### Code Snippet
```javascript
// src/middleware/logger.js

const express = require('express');
const app = express();

// Request middleware
app.use((req, res, next) => {
  console.log(`Request received: ${req.method} ${req.url}`);
  next();
});

// Response middleware
app.use((req, res, next) => {
  console.log(`Response sent: ${res.statusCode}`);
  next();
});

app.get('/', (req, res) => {
  res.send('Hello World!');
});

const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

---

## Pure Functions

### What
A function that always returns the same output given the same inputs and has no side effects.

### Characteristics
- **Deterministic:** Always returns the same output for the same inputs.
- **No side effects:** Does not modify external state or have observable effects.
- **Immutable:** Does not modify its own state or the state of its inputs.

### Benefits
- **Predictable behavior:** Easy to reason about and test.
- **Reusable:** Can be safely used in any context without fear of side effects.
- **Composable:** Can be combined with other pure functions to create more complex functions.

### Example
#### Scenario
A simple pure function that adds two numbers.

#### Code Snippet
```javascript
// src/utils/pureFunctions.js

function add(a, b) {
  return a + b;
}

module.exports = { add };
```

---

## Non-Pure Functions

### Example
#### Scenario
A function that generates a random number.

#### Code Snippet
```javascript
// src/utils/nonPureFunctions.js

function getRandomNumber() {
  return Math.random();
}

module.exports = { getRandomNumber };
```