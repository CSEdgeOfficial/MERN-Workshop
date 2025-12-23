
# Getting Started with React (6 Hours)

---

##  Learning Goals

By the end of Day 2, you will:

- Understand **React components**
    
- Learn **JSX**
    
- Use **props** and **state**
    
- Handle **button clicks & forms**
    
- Style components
    
- Fetch data with `useEffect`
    
- Create **reusable components**
    
- Navigate pages with **React Router**
    
- Share state using **useContext**
    
- Organize folders like real projects
    

---
## 1️⃣ What is React?

- React is a **JavaScript library** used to build **User Interfaces (UI)**
    
- Developed by **Facebook**
    
- Uses **component-based architecture**
    
- Makes **Single Page Applications (SPA)**
    

---

## 2️⃣ What is a Component?

- A component is a **reusable piece of UI**
    
- Written as a **JavaScript function**
    
- Components return **JSX**

---

## 1. Understanding Components 

### What is a Component?

A **component** is a reusable piece of UI.

### Simple Component

```jsx
function Welcome() {
  return <h2>Welcome to React</h2>;
}

export default Welcome;
```

### Using a Component

```jsx
import Welcome from "./Welcome";

function App() {
  return <Welcome />;
}
```

---

##  2. JSX (JavaScript + HTML) 

JSX lets you write **HTML inside JavaScript**.

### JSX Example

```jsx
const name = "Alex";

function App() {
  return <h1>Hello, {name}</h1>;
}
```

 `{}` is used to write JavaScript inside JSX.

---

## 3. Props (Passing Data)

Props are used to **send data from parent to child**.

### Parent Component

```jsx
<Greeting name="Sam" />
```

### Child Component

```jsx
function Greeting(props) {
  return <h2>Hello {props.name}</h2>;
}
```

---

## 4. State (useState)

State stores **changing data**.

### Counter Example

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
    </>
  );
}
```

---

##  5. Handling Button Clicks 

### Simple Click

```jsx
<button onClick={() => alert("Button clicked!")}>
  Click Me
</button>
```

---

##  6. Handling Form Inputs 

### Input with State

```jsx
import { useState } from "react";

function Form() {
  const [name, setName] = useState("");

  return (
    <>
      <input 
        type="text"
        placeholder="Enter name"
        onChange={(e) => setName(e.target.value)}
      />
      <p>Your name: {name}</p>
    </>
  );
}
```

---

##  7. Styling Components 

### CSS File

```css
.title {
  color: blue;
  font-size: 24px;
}
```

### Using CSS

```jsx
import "./App.css";

<h1 className="title">Styled Text</h1>
```

---

### 8. Tailwind CSS Example

1. **Install Tailwind css**
   ```shell
   npm install tailwindcss @tailwindcss/vite
   ```
   
2. **Update vite.config.ts**
 ```js
import { defineConfig } from 'vite'
import react from "@vitejs/plugin-react";
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [
	react(), tailwindcss(),
  ],
})
      ```

```jsx
<h1 className="text-2xl text-red-500 font-bold">
  Hello Tailwind
</h1>
```

 Tailwind uses **utility classes**.

---

##  9. useEffect (Side Effects) 

Used for:

- Fetching data
    
- Running code when page loads
    

### Example

```jsx
import { useEffect } from "react";

useEffect(() => {
  console.log("Component Loaded");
}, []);
```

`[]` means **run once**.

---

##  10. Data Fetching Example 

```jsx
import { useEffect, useState } from "react";

function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

---

##  Reusable Components 

### Button Component

```jsx
function Button({ text }) {
  return <button>{text}</button>;
}
```

### Use It Anywhere

```jsx
<Button text="Login" />
<Button text="Register" />
```

---

## 11. Page Navigation (React Router) 

### Install

```bash
npm install react-router-dom
```

### Basic Setup

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

### Navigation Links

```jsx
import { Link } from "react-router-dom";

<Link to="/">Home</Link>
<Link to="/about">About</Link>
```

---

## 12. State Sharing (useContext) 🧠

### Create Context

```jsx
import { createContext } from "react";

export const UserContext = createContext();
```

### Provide Context

```jsx
<UserContext.Provider value="Alex">
  <Profile />
</UserContext.Provider>
```

### Use Context

```jsx
import { useContext } from "react";
import { UserContext } from "./UserContext";

function Profile() {
  const user = useContext(UserContext);
  return <h2>User: {user}</h2>;
}
```

---

## 13. Folder Structure 📁

### Simple Real-World Structure

```
src/
 ├─ components/
 ├─ pages/
 ├─ context/
 ├─ App.jsx
 └─ main.jsx
```

 Keeps code **clean and organized**.


---

## 🧠 ONE-LINE EXAM ANSWERS

| Question          | Answer                            |
| ----------------- | --------------------------------- |
| What is JSX?      | JSX allows HTML inside JavaScript |
| What is state?    | State stores dynamic data         |
| What is props?    | Props pass data to components     |
| useEffect use?    | Runs side effects                 |
| React Router use? | Page navigation                   |
| useContext use?   | Global state sharing              |