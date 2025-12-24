Below is a **clear, step-by-step guide to perform CRUD operations in Mongoose** (Create, Read, Update, Delete) using **Node.js + Express + MongoDB**.
This is the **standard way used in real MERN projects**.

---

## 🔹 1. Install Required Packages

```bash
npm init -y
npm install express mongoose cors dotenv
```

---

## 🔹 2. Connect MongoDB using Mongoose

📁 **config/db.js**

```js
const mongoose = require("mongoose");

const connectDB = async () => {
  try {
    await mongoose.connect(process.env.MONGO_URI);
    console.log("MongoDB Connected");
  } catch (error) {
    console.error(error);
    process.exit(1);
  }
};

module.exports = connectDB;
```

📁 **server.js**

```js
require("dotenv").config();
const express = require("express");
const connectDB = require("./config/db");

const app = express();
app.use(express.json());

connectDB();

app.listen(5000, () => {
  console.log("Server running on port 5000");
});
```

---

## 🔹 3. Create a Mongoose Model (Schema)

📁 **models/User.js**

```js
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  age: Number,
}, { timestamps: true });

module.exports = mongoose.model("User", userSchema);
```

---

## 🔹 4. CRUD Operations in Express Routes

📁 **routes/userRoutes.js**

```js
const express = require("express");
const User = require("../models/User");

const router = express.Router();
```

---

## 🟢 CREATE (POST)

```js
router.post("/users", async (req, res) => {
  try {
    const user = await User.create(req.body);
    res.status(201).json(user);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
});
```

---

## 🔵 READ (GET)

### Get All Users

```js
router.get("/users", async (req, res) => {
  const users = await User.find();
  res.json(users);
});
```

### Get User by ID

```js
router.get("/users/:id", async (req, res) => {
  const user = await User.findById(req.params.id);
  res.json(user);
});
```

---

## 🟡 UPDATE (PUT)

```js
router.put("/users/:id", async (req, res) => {
  const updatedUser = await User.findByIdAndUpdate(
    req.params.id,
    req.body,
    { new: true }
  );
  res.json(updatedUser);
});
```

---

## 🔴 DELETE (DELETE)

```js
router.delete("/users/:id", async (req, res) => {
  await User.findByIdAndDelete(req.params.id);
  res.json({ message: "User deleted successfully" });
});
```

---

## 🔹 5. Use Routes in Server

📁 **server.js**

```js
const userRoutes = require("./routes/userRoutes");
app.use("/api", userRoutes);
```

---

## 🔹 6. Test CRUD Using Postman

| Method | URL            | Description   |
| ------ | -------------- | ------------- |
| POST   | /api/users     | Create user   |
| GET    | /api/users     | Get all users |
| GET    | /api/users/:id | Get one user  |
| PUT    | /api/users/:id | Update user   |
| DELETE | /api/users/:id | Delete user   |

---

## 🔹 Common Mongoose CRUD Methods (IMPORTANT)

| Operation | Method                      |
| --------- | --------------------------- |
| Create    | `Model.create()`            |
| Read All  | `Model.find()`              |
| Read One  | `Model.findById()`          |
| Update    | `Model.findByIdAndUpdate()` |
| Delete    | `Model.findByIdAndDelete()` |

---
