# React Concepts

## Components

### What
Reusable UI pieces.

### Why
- Modular code
- Reusable code
- Maintainable code

### Where
- **ProductCard:** Reusable for each product.

#### Code Snippet
```jsx
// src/components/ProductCard.js

import React from 'react';

const ProductCard = ({ name, price }) => {
  return (
    <div className="product-card">
      <h2>{name}</h2>
      <p>{price}</p>
    </div>
  );
};

export default ProductCard;
```

---

## Routes

### What
Navigation paths in a React app.

### Why
- Enable client-side routing
- Allow URL changes without full page reloads

### Where
- **Home page:** `/`
- **About page:** `/about`
- **Product page:** `/products/:id`

#### Code Snippet
```jsx
// src/App.js

import React from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';
import Product from './components/Product';

const App = () => {
  return (
    <Router>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
        <Route path="/products/:id" component={Product} />
      </Switch>
    </Router>
  );
};

export default App;
```

---

## State

### What
Data that changes within a component.

### Why
- Needed to update the UI in response to user interactions
- Allows components to remember information

### Where
- Form input values
- Checkbox checked/unchecked status
- Counter values

#### Code Snippet
```jsx
// src/components/Counter.js

import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default Counter;
```

---

## Props

### What
Short for "properties", read-only data passed to components.

### Why
- Allow components to receive data from their parents
- Enable component customization and reuse

### Where
- Passing a product's name and price to a ProductCard component

#### Code Snippet
```jsx
// src/components/ProductList.js

import React from 'react';
import ProductCard from './ProductCard';

const ProductList = () => {
  const products = [
    { name: 'Product 1', price: '$10' },
    { name: 'Product 2', price: '$20' },
  ];

  return (
    <div>
      {products.map((product, index) => (
        <ProductCard key={index} name={product.name} price={product.price} />
      ))}
    </div>
  );
};

export default ProductList;
```

---

## Hooks

### What
Functions that let you "hook into" React state and lifecycle from functional components.

### Why
- Enable state and side effects in functional components
- Provide an alternative to class components

### Where
#### Scenario
A weather app that displays the current temperature and updates it every hour.

#### Use Case
Use the `useState` hook to store the current temperature and the `useEffect` hook to fetch new temperature data every hour.

#### Code Snippet
```jsx
// src/components/Weather.js

import React, { useState, useEffect } from 'react';

const Weather = () => {
  const [temperature, setTemperature] = useState(null);

  useEffect(() => {
    const fetchTemperature = async () => {
      const response = await fetch('https://api.weatherapi.com/v1/current.json?key=YOUR_API_KEY&q=London');
      const data = await response.json();
      setTemperature(data.current.temp_c);
    };

    fetchTemperature();
    const interval = setInterval(fetchTemperature, 3600000); // Update every hour

    return () => clearInterval(interval);
  }, []);

  return (
    <div>
      <p>Current Temperature: {temperature}°C</p>
    </div>
  );
};

export default Weather;
```

---

## Higher-Order Functions

### What
Functions that take other functions as arguments or return functions as output.

### Why
- Enable function composition and abstraction
- Allow for more flexible and reusable code

### Where
#### Scenario
Building an e-commerce application with different types of discounts:
- 10% off for students
- 20% off for seniors
- Buy one get one free for certain products

#### Use Case
Use a higher-order function to create a discount calculator that takes a discount function as an argument.

#### Code Snippet
```jsx
// src/utils/discounts.js

function calculateDiscount(price, discountFunc) {
  return discountFunc(price);
}

function studentDiscount(price) {
  return price * 0.9;
}

function seniorDiscount(price) {
  return price * 0.8;
}

function buyOneGetOneFree(price) {
  return price / 2;
}

const productPrice = 100;
const studentDiscountedPrice = calculateDiscount(productPrice, studentDiscount);
const seniorDiscountedPrice = calculateDiscount(productPrice, seniorDiscount);
const bogofDiscountedPrice = calculateDiscount(productPrice, buyOneGetOneFree);

export { calculateDiscount, studentDiscount, seniorDiscount, buyOneGetOneFree };
```

---

## Axios

### What
A promise-based HTTP client for making requests to APIs and servers.

### Why
- Simplifies making HTTP requests and handling responses
- Provides a simple and intuitive API for making requests
- Supports promises and async/await syntax

### Where
#### Scenario
Making a GET request to a JSONPlaceholder API to fetch a list of users.

#### Use Case
Use Axios to make a GET request to the API and log the response data.

#### Code Snippet
```jsx
// src/api/fetchUsers.js

import axios from 'axios';

const fetchUsers = async () => {
  try {
    const response = await axios.get('https://jsonplaceholder.typicode.com/users');
    console.log(response.data);
  } catch (error) {
    console.error('Error fetching users:', error);
  }
};

fetchUsers();
```