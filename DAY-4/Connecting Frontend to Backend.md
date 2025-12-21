
---

# Day 4: Connecting Frontend to Backend with Database (6 Hours)

---

## Learning Goals

By the end of Day 4, you will:

- Connect React frontend to Express backend
    
- Send GET and POST requests
    
- Store and fetch data from MongoDB
    
- Submit forms from UI to database
    
- Understand authentication flow
    
- Store users securely using bcrypt
    
- Authenticate users using JWT
    
- Plan login/signup properly
    
- Use separate frontend and backend repositories
    

---

# PART 1: Normal Frontend → Backend → Database Flow

---

## 1. MongoDB User Model

### `models/User.js`

```js
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  password: String
});

module.exports = mongoose.model("User", userSchema);
```

---

## 2. Basic Backend Setup

### `server.js`

```js
const express = require("express");
const mongoose = require("mongoose");
const User = require("./models/User");

const app = express();
app.use(express.json());

mongoose.connect("YOUR_MONGODB_URI")
  .then(() => console.log("MongoDB connected"))
  .catch(err => console.log(err));

app.listen(5000, () => {
  console.log("Server running on port 5000");
});
```

---

## 3. Saving Data to MongoDB (NO AUTH)

### POST User (Plain Data)

```js
app.post("/api/users", async (req, res) => {
  const user = new User(req.body);
  await user.save();

  res.json({ message: "User saved", user });
});
```

---

## 4. Fetching Data from MongoDB

```js
app.get("/api/users", async (req, res) => {
  const users = await User.find();
  res.json(users);
});
```

---

## 5. React: Sending Data to Backend

```jsx
import { useState } from "react";
import axios from "axios";

function AddUser() {
  const [name, setName] = useState("");

  const submitHandler = async (e) => {
    e.preventDefault();

    await axios.post("http://localhost:5000/api/users", {
      name
    });

    setName("");
  };

  return (
    <form onSubmit={submitHandler}>
      <input
        placeholder="Name"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <button>Add</button>
    </form>
  );
}

export default AddUser;
```

---

# PART 2: Signup & Login (PLAIN TEXT, STORED IN DB)

---

## 6. Signup API (Insecure, for learning)

```js
app.post("/api/signup", async (req, res) => {
  const { email, password } = req.body;

  const user = new User({ email, password });
  await user.save();

  res.json({ message: "User registered" });
});
```

---

## 7. Login API (Plain Password)

```js
app.post("/api/login", async (req, res) => {
  const { email, password } = req.body;

  const user = await User.findOne({ email });

  if (!user || user.password !== password) {
    return res.status(400).json({ message: "Invalid credentials" });
  }

  res.json({ message: "Login successful" });
});
```

This works but is **not secure**.

---

# PART 3: Securing Passwords with bcrypt (STORED HASH)

---

## 8. Install bcrypt

```bash
npm install bcryptjs
```

---

## 9. Signup API with bcrypt + MongoDB

```js
const bcrypt = require("bcryptjs");

app.post("/api/signup", async (req, res) => {
  const { email, password } = req.body;

  const hashedPassword = await bcrypt.hash(password, 10);

  const user = new User({
    email,
    password: hashedPassword
  });

  await user.save();

  res.json({ message: "User registered securely" });
});
```

---

## 10. Login API with bcrypt + MongoDB

```js
app.post("/api/login", async (req, res) => {
  const { email, password } = req.body;

  const user = await User.findOne({ email });

  if (!user) {
    return res.status(400).json({ message: "User not found" });
  }

  const isMatch = await bcrypt.compare(password, user.password);

  if (!isMatch) {
    return res.status(400).json({ message: "Invalid credentials" });
  }

  res.json({ message: "Login successful" });
});
```

---

# PART 4: Adding JWT (AUTH TOKEN STORED CLIENT-SIDE)

---

## 11. Install JWT

```bash
npm install jsonwebtoken
```

---

## 12. Login API with JWT + Database

```js
const jwt = require("jsonwebtoken");

app.post("/api/login", async (req, res) => {
  const { email, password } = req.body;

  const user = await User.findOne({ email });

  if (!user) {
    return res.status(400).json({ message: "User not found" });
  }

  const isMatch = await bcrypt.compare(password, user.password);

  if (!isMatch) {
    return res.status(400).json({ message: "Invalid credentials" });
  }

  const token = jwt.sign(
    { userId: user._id },
    "SECRET_KEY",
    { expiresIn: "1h" }
  );

  res.json({ token });
});
```

---

## 13. Frontend: Store JWT Token

```js
localStorage.setItem("token", res.data.token);
```

---

## 14. Authentication Flow (Final)

```
Signup → bcrypt hash → save in MongoDB
Login → bcrypt compare → JWT created
Frontend → stores token
Token → used for protected APIs
```

---

## 15. Basic Error Handling

```js
if (!email || !password) {
  return res.status(400).json({ message: "All fields required" });
}
```

---

