# Lab: Getting Started with useState – A Simple Counter

Welcome to your first React state lab! In this micro-lab, you’ll build a simple counter using `useState`. You’ll learn how to update state and trigger re-renders based on user actions.

## Learning Objectives

By the end of this lab, you'll be able to:

- Use the `useState` hook in a functional component
- Update and display state on the screen
- Handle button clicks in React
- Understand how state re-renders the UI

## What You'll Build

A simple app with:

- A number displayed on screen
- A "+" button to increase the number
- A "-" button to decrease the number
- (Optional) A "Reset" button

## Estimated Time

15–25 minutes

## Step 1: Setup Your React App

You can use Vite to start. Here’s how to use Vite:

```bash
npm create vite@latest use-state-counter
select react
select javascript
cd use-state-counter
npm install
npm run dev
```

## Step 2: Set Up Your Component

When you create the react app you will be met with alot of boiler plate code, we dont need that so you can
clear `App.jsx`, `App.css`, and `index.css`. LEAVE `main.jsx` alone.

Navigate to `src/App.jsx`.

Replace the code with a basic functional component scaffold:

```jsx
import "./App.css";
function App() {
  return (
    <div className="app">
      <h1 className="title">Counter App</h1>
      <p className="count">Count: ???</p>
      <div className="buttons">
        <button className="btn increment">+</button>
        <button className="btn decrement">-</button>
      </div>
    </div>
  );
}

export default App;
```

Check this github folder for the premade App.css file. Copy paste to yours.

## Step 3: Add State with useState

Your goal: Add state to track the counter value. Do this in `App.jsx`

Try on your own first. Then open hints if you're stuck.

Remeber what useState is and how you would first define it in your file?

<details>
<summary>Hint</summary>

Use the `useState` hook at the top of your component:

```js
const [count, setCount] = useState(0);
```

Make sure to import `useState` from React. What variable is used to actually display the count?

</details>

<details>
<summary>Full Solution</summary>

```jsx
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Counter App</h1>
      <p>Count: {count}</p>
      <button>+</button>
      <button>-</button>
    </div>
  );
}

export default App;
```

</details>

## Step 4: Add Functionality to the Buttons

Your goal: Make the "+" button increase the count, and the "-" button decrease it. Think what event handler works for this? and what part of the hook is made for this?

<details>
<summary>Hint</summary>

Add an `onClick` prop to each button. Use `setCount(count + 1)` and `setCount(count - 1)`.

</details>

<details>
<summary>Full Solution</summary>

```jsx
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Counter App</h1>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
      <button onClick={() => setCount(count - 1)}>-</button>
    </div>
  );
}

export default App;
```

</details>

## Step 5 (Optional): Add a Reset Button

<details>
<summary>Hint</summary>

Just add another `<button>` with `setCount(0)` on click.

</details>

<details>
<summary>Full Solution</summary>

```jsx
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Counter App</h1>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
      <button onClick={() => setCount(count - 1)}>-</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}

export default App;
```

</details>

## Bonus Challenges

Try these if you finish early:

- Disable the “-” button when the count is 0
- Show a different message when the count is 0 (e.g., "Let's start counting!")
- Make the text color change depending on the count (e.g., red if negative)

## Wrap-Up: What You Learned

- How to import and use the `useState` hook
- How state variables trigger re-renders
- How to update state using event handlers
- The core idea of React interactivity: state drives UI
