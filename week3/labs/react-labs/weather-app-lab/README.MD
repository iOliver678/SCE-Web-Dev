# Lab: Getting Started API calls – Building a Weather App

In this lab, you’ll learn how to fetch live weather data from the OpenWeather API. This will teach you how to handle dynamic rendering in React, work with **async/await**, and chain multiple API calls. You’ll also learn how to manage state for loading, error handling, and rendering API responses.

## Learning Objectives

By the end of this lab, you’ll be able to:

- Fetch weather data from an external API
- Use `async/await` and `fetch` to handle asynchronous requests
- Convert a city name or ZIP code into latitude/longitude using the Geocoding API
- Pass the coordinates into the One Call API to get the actual weather
- Manage loading and error states for a clean user experience

## What You’ll Build

A simple weather app that:

- Take in user input, state and country (San Jose, Ca).
- Calls the OpenWeather Geocoding API to convert the location into coordinates
- Uses the One Call API to fetch weather data
- Displays the current temperature and conditions
- Handles loading and error states gracefully

## Estimated Time

60 minutes

## Step 1: Setup Your React App

We’ll start fresh with Vite:

```bash
npm create vite@latest use-effect-weather
select react
select javascript
cd use-effect-weather
npm install
npm run dev
```

## Step 2: Clean Up Boilerplate

As before, clean out:

- `App.jsx`
- `App.css`
- `index.css`

Copy and paste the `App.css` file to yours. Make sure to correctly add the components to their classes, after each step, check the full solution to make sure you are in touch with the code.

Leave `main.jsx` alone.

Replace `App.jsx` with a scaffold:

```jsx
import "./App.css";

function App() {
  return (
    <div className="app">
      <h1 className="title">Weather App</h1>
      <p>Temperature: </p>
      <p>Condition: </p>
    </div>
  );
}

export default App;
```

## Step 3: Import useState

Lets start off by importing useState. We’ll need it to fetch data and store results. Then create 4 state hooks. `cityName`, `weather`, `loading`, and `error`. Set them to null, null, null, False, and null.

<details>
<summary>Hint</summary>

Add this to the top of your file:

```js
import { useState } from "react";
```

Then create 5 pieces of state: `cityName`, `weather`, `loading`, `error`.

</details>

<details>
<summary>Full Solution</summary>

```jsx
import { useState } from "react";
import "./App.css";

function App() {
  const [weather, setWeather] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);
  const [cityName, setCityName] = useState(null);
  return (
    <div className="app">
      <h1 className="title">Weather App</h1>
      <p>Temperature: </p>
      <p>Condition: </p>
    </div>
  );
}

export default App;
```

</details>

<br>

Now we are going to set up to be able to take in user input. So lets create an input element along with a button to be able to send this info out. You will want to wrap this in a form so you have control over when you send the input. For simplicity we are only take in a citys name not the country, we will be hardcoding the country.

Create an input element and assign it the value of the city hook. Make it a type="text" and also link it with the onChange event listener to update the setCityName. Now make the button an submit type so when you submit the form it all updates. If you have never done this before dont worry, here is what it should look like:

```jsx
import { useState } from "react";
import "./App.css";

function App() {
  const [weather, setWeather] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);
  const [cityName, setCityName] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault(); // prevents page refresh
    console.log("City submitted:", cityName);
    // later you’ll fetch weather API here
  };

  return (
    <div className="app">
      <h1 className="title">Weather App</h1>
      <p>Temperature: </p>
      <p>Condition: </p>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          value={cityName}
          onChange={(e) => setCityName(e.target.value)}
          placeholder="Enter city or ZIP"
        />
        <button type="submit">Get Weather</button>
      </form>
    </div>
  );
}

export default App;
```

Bellow is a full explanation of what we just did. Take the time to understand it.

<details>
<summary>Explanation</summary>

### Understanding Forms, State, and Event Handling in React

### Forms in React

- A `<form>` groups inputs and buttons together.
- By default, submitting a form (via button click or pressing Enter) triggers a **page reload**.
- In React, we prevent that reload and handle the logic ourselves with an `onSubmit` handler.

### Controlled Components

- Inputs in React are usually **controlled components**.
- This means the input value is tied to React state using `useState`.
- Example:
  - `const [city, setCity] = useState("");`
  - `value={city}` → the input always shows the latest state.
  - `onChange={(e) => setCity(e.target.value)}` → updates the state whenever the user types.

### Event Handling

- `onChange` is used on inputs to track what the user types.
- `onSubmit` is used on forms to handle when the form is submitted.
- A submit handler typically calls `e.preventDefault()` to stop the page reload.

### Submit Buttons

- A `<button type="submit">` inside a form automatically triggers the form’s `onSubmit`.
- This allows one central handler for form submission, instead of adding `onClick` directly to the button.

### The Flow

1. User types → `onChange` updates state.
2. State holds the latest input value.
3. User submits → `onSubmit` runs, `e.preventDefault()` stops reload.
4. The submit handler can now use the state value (e.g., call an API).

</details>

## Step 4: Call the Geocoding API

OpenWeather’s One Call API requires coordinates, not city names. Go to [Open Weather API](https://openweathermap.org/) and make a free account to get an API Key.

So first we call the Geocoding API:

```
https://api.openweathermap.org/geo/1.0/direct?q=${cityName},US&limit=1&appid=APIkey
```

This is the url that we will be using to call the api, take a look at the docs on the Geocoding API. It says it needs a city name and a country. We are hard coding the country, and passing in the cityName dynamically, template literal with a $ at the start of our var, therefore the brackets. In a url, you pass in params by indicating with a ?.

This returns JSON with latitude (`lat`) and longitude (`lon`).
This is the actual payload.

```
[
  {
    "name": "San Jose",
    "local_names": {
      "oc": "San José",
      "en": "San Jose",
      "ar": "سان خوسيه",
      "am": "ሳን ሆዜ",
      "es": "San José",
      "vi": "San Jose",
      "gl": "San Xosé",
      "uk": "Сан-Хосе",
      "zh": "聖荷西",
      "pt": "San José",
      "ru": "Сан-Хосе",
      "eo": "San-Joseo"
    },
    "lat": 37.3361663,
    "lon": -121.890591,
    "country": "US",
    "state": "California"
  }
]
```

We now want to set up the API call, we can do this with the on submit funtion. Handle submit in our case:

```jsx
const handleSubmit = async (e) => {
  try {
    const geoRes = await fetch(
      `https://api.openweathermap.org/geo/1.0/direct?q=${cityName},US&limit=1&appid=YOUR_API_KEY`
    );
    const geoData = await geoRes.json();
    console.log(geoData); // check what it returns
  } catch (err) {
    console.error(err);
  }
};
```

This is how you set up an api call in jsx.

<details>
<summary>Explanation</summary>
Inside it, you wrote an async function with await so you can pause and wait for the API call to finish before moving on. That way you don’t just get a “promise” back, you get the actual JSON data.

So in short:

async/await makes the fetch act step-by-step, so you can easily get the real data.

</details>

<details>
<summary>Hint</summary>

Inside `onSubmit`, create an async function that fetches the geocode data, extracts `lat` and `lon`, and logs them.

</details>

<details>
<summary>Full Solution</summary>

```jsx
import { useState } from "react";
import "./App.css";

function App() {
  const [weather, setWeather] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  const [cityName, setCityName] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();
    if (!cityName) return;
    try {
      const geoRes = await fetch(
        `https://api.openweathermap.org/geo/1.0/direct?q=${cityName},US&limit=1&appid=YOUR_API_KEY`
      );
      const geoData = await geoRes.json();
      console.log(geoData); // check what it returns
    } catch (err) {
      console.error(err);
    }
  };

  return (
    <div className="app">
      <h1 className="title">Weather App</h1>
      <p>Temperature: </p>
      <p>Condition: </p>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          value={cityName}
          onChange={(e) => setCityName(e.target.value)}
          placeholder="Enter city or ZIP"
        />
        <button type="submit">Get Weather</button>
      </form>
    </div>
  );
}

export default App;
```

</details>
<br>
Looking at the data you are given, now we want to unpack this using the bracket notation we have learned. Remeber the payload, or check the console log. Unpack and assign to some variables `lat` and `lon` and console log to make sure they are correct.
<br>
<br>
<details>
<summary>Here is how</summary>

```jsx
const geoRes = await fetch(
  `https://api.openweathermap.org/geo/1.0/direct?q=${cityName},US&limit=1&appid=YOUR_API_KEY`
);
const geoData = await geoRes.json();
const { lat, lon } = geoData[0];
```

</details>

## Step 5: Use the Coordinates to Call the Current Weather API

Once you have `lat` and `lon`, plug them into the (Current Weather Api)[https://openweathermap.org/current]:

```
https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&units=imperial&appid=APIKEY
```

Call the api, console log it to check the payload or go and check the offical docs so you know what it will look like. Assign it and unpack it like we have done before.

Once you assign it to your weather variable hook, then can use that hook to render it, using dot notation inline the elements. We only want to display the location, temperature and the condition. Go take a look at the expected payload so you can use asign the data to the hook variable we have, so you can use it within our elements.

<details>
<summary>Hint</summary>

After fetching coords, immediately call the One Call API inside the same function.

</details>

<details>
<summary>Full Solution</summary>

```jsx
import { useState } from "react";
import "./App.css";

function App() {
  const [weather, setWeather] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  const [cityName, setCityName] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();
    if (!cityName) return;
    try {
      // Step 1: Get coords
      const geoRes = await fetch(
        `https://api.openweathermap.org/geo/1.0/direct?q=${cityName},US&limit=1&appid=APIKEY`
      );

      const geoData = await geoRes.json();
      if (!geoData.length) throw new Error("City not found");
      const { lat, lon } = geoData[0];


      // Step 2: Get weather
      const weatherRes = await fetch(
        `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&units=imperial&appid=APIKEY`
      );
      if (!weatherRes.ok) {
        throw new Error("Weather request failed");
      }
      const weatherData = await weatherRes.json();
      setWeather(weatherData);
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  }

  if (loading) return <p>Loading weather...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <div className="app">
      <h1 className="title">Weather App</h1>
        <p>Location: {weather.name}, {weather.sys country}</p>
        <p>Temperature: {weather.main.temp}°F</p>
        <p>Condition: {weather.weather[0].description}</p>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          value={cityName}
          onChange={(e) => setCityName(e.target.value)}
          placeholder="Enter city or ZIP"
        />
        <button type="submit">Get Weather</button>
      </form>
    </div>
  );
}

export default App;
```

</details>

## Step 6: Test It

- Replace `YOUR_API_KEY` with your actual OpenWeather API key.
- Start your dev server with `npm run dev`.
- You should see a loading message, then the current temperature and condition for San Jose when you test the input.

## Bonus Challenges

Try these if you finish early:

- Let the user type a city name instead of hardcoding San Jose
- Add a button to refetch weather data
- Convert temperatures to Fahrenheit and toggle between units

## Wrap-Up: What You Learned

- How to chain two API requests: Geocoding first, then One Call
- How to use `async/await` for cleaner asynchronous code
- How to manage `loading` and `error` states
- How to fetch and render real-world weather data into a React component
