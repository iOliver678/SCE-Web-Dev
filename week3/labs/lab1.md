# Lab: Build a To-Do List UI (React.js)

## Overview

In this lab, you’ll build the **frontend** for a basic To-Do List web app using **React.js**. You’ll simulate data that would normally come from an API and focus on how to use **props**, **component structure**, and **event handling** to create a working UI.

Your app will support:

- Displaying a list of to-dos
- Adding new to-dos
- Editing to-dos
- Deleting to-dos

**Note:** For now, you won't fetch data from the server or persist it. That comes later when we learn about state and useEffect.

---

## Learning Objectives

By the end of this lab, you should be able to:

- Create a React app using Vite
- Build a UI using props and simple component structure
- Simulate API data using a static array
- Handle click and input events in React

---

## Step 0: Setup

Open your terminal and run the following to create your project.

```bash
npm create vite@latest
cd react-todo-ui
npm install
npm run dev
```

---

## Step 1: Simulate Your API Data

In your `App` component:

- [ ] Create an array of task objects (each with `id` and `task`)
- [ ] Treat this array like data returned from an API
- [ ] You’ll use it as the data source for your list

---

## Step 2: Create the `TodoList` Component

In a new file called `TodoList.jsx`:

- [ ] Make a component that receives:
  - [ ] The array of tasks
  - [ ] A delete handler function
  - [ ] An edit handler function
- [ ] Render each task inside a list
- [ ] Include "Edit" and "Delete" buttons next to each task
- [ ] Call the correct handler when each button is clicked

---

## Step 3: Use `TodoList` in `App.jsx`

Back in `App.jsx`:

- [ ] Add your main div to a class called container - `className="container"`
- [ ] Import and render the `TodoList` component
- [ ] Pass in as props to our `TodoList` component:
  - [ ] The task array
  - [ ] A `handleDelete` function that logs the task ID - just create and log, no logic
  - [ ] A `handleEdit` function that logs the task ID - just create and log, no logic
- [ ] Test that clicking the buttons prints the correct ID

---

## Step 4: Add a New Task Input

In the `App.jsx` UI:

- [ ] Add an `<input>` element for typing a new task
- [ ] Add an "Add" button next to the input
- [ ] Important - Wrap your input and button in a div and add that div to `className="input-row"`
- [ ] When clicked, log the text from the input field
- [ ] You don’t need to store or display the new task yet

---

## Step 5: Simulate Add/Edit/Delete

Manually update the array in your code:

- [ ] Add a new item to the array
- [ ] Change the text of an existing item
- [ ] Remove an item from the array

Each time:

- [ ] Save the file
- [ ] Refresh the browser
- [ ] Confirm that your updates show up

This simulates what `useState` will eventually do dynamically.

---

## Bonus: Make a Task Editable

If you finish early and want a challenge:

- [ ] Try rendering an `<input>` instead of a `<p>` when "Edit" is clicked
- [ ] Use a temporary variable (not state) to simulate "editing mode"
- [ ] This will be much easier once you learn `useState`

---

## What You Learned

- [ ] How to simulate API data using a hardcoded array
- [ ] How to pass data and actions through props
- [ ] How React breaks UI into reusable components
- [ ] Why state is necessary for interactivity

---
