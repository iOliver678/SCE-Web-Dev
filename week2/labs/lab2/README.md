# Lab: Build a To-Do List API (Express.js)

## Overview

In this lab, we’ll build the backend for a basic To-Do List web app using Node.js and Express. The goal is to create a simple REST API that allows users to:

- View all to-do items
- Add a new to-do item
- Delete an existing to-do item

This is a great first project if you're just learning how web servers work. You’ll get hands-on experience with routing, HTTP methods, and testing using Postman.

## Learning Objectives

By the end of this lab, you will be able to:

- Initialize a Node.js project with `npm`
- Set up a basic Express server
- Define GET, POST, and DELETE routes
- Use an in-memory array to store data temporarily (instead of using a database)
- Use Postman to test your API endpoints

## Let's Get Started (60–75 mins)

### Step 0: Setup

#### Your Turn

- Make a new project directory:

```bash
mkdir express-todo-api
cd express-todo-api
```

- Initialize a Node.js project:

```bash
npm init -y
```

This creates a `package.json` file, which will manage your project's dependencies (like Express) and metadata.

- Install Express:

```bash
npm install express
```

Checkpoint  
You should now have a `package.json` file and a `node_modules` folder in your project directory. This means Express has been successfully installed.

### Step 1: Create Your Server File

Create a new file in the root of your project:

```bash
touch index.js
```

This file will act as the main entry point for your backend — it’s where you'll write all the logic for your Express server.

### Step 2: Set Up the Express Server

Open `index.js` and write the following starter code:

```js
const express = require("express");
const app = express();

const PORT = 3000;

// Middleware to parse JSON
app.use(express.json());

app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

Explanation:

- `require('express')`: Loads the Express library.
- `express()`: Creates an instance of the Express application.
- `app.use(express.json())`: Tells Express to automatically parse any incoming JSON in the body of requests.
- `app.listen(...)`: Starts the server and tells it to listen on a specific port (3000 in this case).

Checkpoint  
Your Express server is now ready to receive routes and process requests.

### Step 3: Create In-Memory To-Do List

Add this array above the `app.listen` line:

```js
let todos = [
  { id: 1, task: "Learn Node.js" },
  { id: 2, task: "Build a REST API" },
];
```

This array will act as your fake "database." Since we aren’t using a real database yet, this is where we'll temporarily store the to-do items in memory.

Note: If the server restarts, all the data in this array will be lost. That's because it's stored in RAM, not in a file or database.

### Step 4: Define Your First Route – GET `/todos`

```js
app.get("/todos", (req, res) => {
  res.json(todos);
});
```

Explanation:

- `app.get(...)`: This is how you define a GET route in Express.
- `/todos`: This is the path. When a client makes a request to this path, this function will run.
- `res.json(todos)`: Sends the `todos` array back to the client as JSON.

Checkpoint  
Start your server with:

```bash
node index.js
```

Then visit:  
http://localhost:3000/todos  
You should see the list of to-dos in your browser.

### Step 5: Define POST `/todos` Route

```js
app.post("/todos", (req, res) => {
  const newTodo = {
    id: Date.now(),
    task: req.body.task,
  };
  todos.push(newTodo);
  res.status(201).json(newTodo);
});
```

Explanation:

- `app.post(...)`: Defines a route that listens for HTTP POST requests.
- `req.body`: Contains the data sent by the client (we get this thanks to `express.json()` middleware).
- `Date.now()`: Gives a unique number to use as an ID.
- `todos.push(...)`: Adds the new to-do item to the array.
- `res.status(201).json(...)`: Sends back the new to-do item with a 201 status (Created).

Checkpoint

Use Postman:

1. Method: `POST`
2. URL: `http://localhost:3000/todos`
3. Body:
   - Choose `raw` and select `JSON` from the dropdown.
   - Paste:

```json
{
  "task": "Try out Postman"
}
```

You should see the new to-do object added and returned in the response.

### Step 6: Define DELETE `/todos/:id` Route

```js
app.delete("/todos/:id", (req, res) => {
  const id = Number(req.params.id);
  todos = todos.filter((todo) => todo.id !== id);
  res.json({ message: `Deleted to-do with id ${id}` });
});
```

Explanation:

- `:id`: This is a route parameter. It allows dynamic values in the URL.
- `req.params.id`: Accesses the `id` provided in the URL.
- `Number(...)`: Converts the ID from a string to a number.
- `.filter(...)`: Removes the matching to-do from the array.

Checkpoint

Use Postman to:

- Method: `DELETE`
- URL: `http://localhost:3000/todos/1`

It should return a confirmation message, and your `GET /todos` route should show that the item is now gone.

## Step 7: Test Everything

Use Postman to confirm:

- GET all to-dos → http://localhost:3000/todos
- POST a new to-do → http://localhost:3000/todos
- DELETE a to-do → http://localhost:3000/todos/:id

## Bonus: Clear All To-Dos (Optional)

Add this if you want to be able to clear out all your to-dos:

```js
app.delete("/todos", (req, res) => {
  todos = [];
  res.json({ message: "All todos cleared." });
});
```

## Full Final Code (index.js)

```js
const express = require("express");
const app = express();
const PORT = 3000;

app.use(express.json());

let todos = [
  { id: 1, task: "Learn Node.js" },
  { id: 2, task: "Build a REST API" },
];

app.get("/todos", (req, res) => {
  res.json(todos);
});

app.post("/todos", (req, res) => {
  const newTodo = {
    id: Date.now(),
    task: req.body.task,
  };
  todos.push(newTodo);
  res.status(201).json(newTodo);
});

app.delete("/todos/:id", (req, res) => {
  const id = Number(req.params.id);
  todos = todos.filter((todo) => todo.id !== id);
  res.json({ message: `Deleted to-do with id ${id}` });
});

// Optional route to delete all todos
// app.delete('/todos', (req, res) => {
//   todos = [];
//   res.json({ message: "All todos cleared." });
// });

app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

## Tools You Used

- Node.js – JavaScript runtime for running server-side code
- Express.js – Framework for building web servers and APIs
- Postman – Tool for testing and sending API requests

## What You Learned

- How to set up an Express server
- How to define RESTful routes (GET, POST, DELETE)
- How to use Postman to test endpoints
- How to simulate data using an in-memory array
- How HTTP methods map to actions (GET → read, POST → create, DELETE → delete)

## Wrap-Up

You’ve built a full-featured API using Express. Understanding these fundamentals is the key to working on real-world backend projects.

```bash
node index.js
```

Then go test all the routes you made.
