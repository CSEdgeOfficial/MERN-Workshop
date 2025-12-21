
# Starting with Node.js, Express & Git (6 Hours)

---

##  Learning Goals

By the end of Day 3, you will:

- Understand **server-side logic**
    
- Create an **Express server**
    
- Build **simple APIs (routes)**
    
- Connect **Express with MongoDB Atlas**
    
- Test APIs using **Postman**
    
- Learn **Git & GitHub basics**
    
- Push code to GitHub
    
- Debug common React & Node errors
    

---

##  Understanding Server-Side Logic 

### What does the server do?

- Receives requests from the client (browser / React)
    
- Processes data
    
- Talks to the database
    
- Sends responses back
    

### Example Flow

```
React App → Express Server → MongoDB → Express → React
```

 Server-side code runs on **Node.js**, not in the browser.

---

## Setting Up a Node + Express Server 

### Step 1: Create Project Folder

```bash
mkdir backend
cd backend
npm init -y
```

### Step 2: Install Express

```bash
npm install express
```

---

### Step 3: Create `server.js`

```js
const express = require("express");
const app = express();

app.listen(5000, () => {
  console.log("Server running on port 5000");
});
```

### Run Server

```bash
node server.js
```

---

##  Creating Simple Routes 

### Basic Route

```js
app.get("/", (req, res) => {
  res.send("API is running");
});
```

### Another Route

```js
app.get("/users", (req, res) => {
  res.send("Users list");
});
```

 Open in browser:

- `http://localhost:5000/`
    
- `http://localhost:5000/users`
    

---

## Sending JSON Responses 

APIs usually send **JSON**, not HTML.

```js
app.get("/api/data", (req, res) => {
  res.json({
    name: "Alex",
    role: "Student"
  });
});
```

---

##  Connecting Express with MongoDB Atlas 

### Step 1: Install Mongoose

```bash
npm install mongoose
```

---

### Step 2: Connect to MongoDB

```js
const mongoose = require("mongoose");

mongoose.connect("YOUR_MONGODB_URL")
  .then(() => console.log("MongoDB Connected"))
  .catch(err => console.log(err));
```

Put this **above `app.listen()`**

---

## Creating a Simple Model 

### `models/User.js`

```js
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  name: String,
  email: String
});

module.exports = mongoose.model("User", userSchema);
```

---

## Fetching Data from MongoDB 

### Sample Route

```js
const User = require("./models/User");

app.get("/users", async (req, res) => {
  const users = await User.find();
  res.json(users);
});
```

---

## Testing APIs Using Postman 

### What is Postman?

A tool to **test APIs** easily.

### Steps:

1. Open Postman
    
2. Choose **GET**
    
3. Enter URL:
    

```
http://localhost:5000/users
```

4. Click **Send**
    

 You should see JSON data.

---

## Why Git is Important 

Git helps you:

- Track code changes
    
- Undo mistakes
    
- Work in teams
    
- Save code online (GitHub)
    

---

## Initializing Git Repository

### Step 1: Initialize Git

```bash
git init
```

### Step 2: Check Status

```bash
git status
```

---

## Making Commits 

### Add Files

```bash
git add .
```

### Commit Changes

```bash
git commit -m "Initial backend setup"
```

---

##  Creating GitHub Repository

### Steps:

1. Go to [https://github.com](https://github.com/)
    
2. Create new repository
    
3. Copy repo URL
    

### Push Code

```bash
git remote add origin REPO_URL
git branch -M main
git push -u origin main
```

---

##  Testing API Workflows in Postman

### Example Flow:

1. POST → Add user
    
2. GET → Fetch users
    
3. PUT → Update user
    
4. DELETE → Remove user
    

This simulates real frontend ↔ backend communication.

---

## Fixing Common Errors

### Console Logs

```js
console.log("Code reached here");
console.log(req.body);
```

---

### Common Node Errors

❌ Port already in use  
✅ Change port or stop other server

❌ Cannot find module  
✅ Run `npm install`

---

### Common React Errors

❌ Component not rendering  
✅ Check `export default`

❌ useState not defined  
✅ Import it:

```js
import { useState } from "react";
```

---

## Debugging Tips

- Use `console.log()` often
    
- Read error messages carefully
    
- Restart server after changes
    
- Check terminal + browser console
    
- Test APIs before connecting React
    

---

## 📁 Backend Folder Structure

```
backend/
 ├─ models/
 ├─ server.js
 ├─ package.json
```
