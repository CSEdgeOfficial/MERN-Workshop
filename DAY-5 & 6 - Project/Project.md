
---

# Day 5–6  Project

## Simple Blogging Website (MERN)

---

## Project Features (What We Will Build)

- User Signup
    
- User Login
    
- Create Blog
    
- View Blogs
    
- Edit Own Blog
    
- Delete Own Blog
    
- JWT-based authentication
    
- MongoDB for storage
    
- Separate frontend and backend
    

---

## Tech Stack Used

- Frontend: React + Axios
    
- Backend: Node.js + Express
    
- Database: MongoDB Atlas + Mongoose
    
- Authentication: bcrypt + JWT
    

---

# PART 1: PROJECT STRUCTURE

---

## Folder Structure

```
blog-project/
 ├─ frontend/
 └─ backend/
```

Create **two separate GitHub repositories**:

- `blog-frontend`
    
- `blog-backend`
    

---

# PART 2: BACKEND IMPLEMENTATION

---

## Step 1: Backend Setup

```bash
mkdir backend
cd backend
npm init -y
npm install express mongoose bcryptjs jsonwebtoken cors
```

---

## Step 2: Basic Server Setup

### `server.js`

```js
const express = require("express");
const mongoose = require("mongoose");
const cors = require("cors");

const app = express();
app.use(express.json());
app.use(cors());

mongoose.connect("YOUR_MONGODB_URI")
  .then(() => console.log("MongoDB connected"));

app.listen(5000, () => {
  console.log("Server running on port 5000");
});
```

---

## Step 3: User Model

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

## Step 4: Blog Model

### `models/Blog.js`

```js
const mongoose = require("mongoose");

const blogSchema = new mongoose.Schema({
  title: String,
  content: String,
  userId: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "User"
  }
});

module.exports = mongoose.model("Blog", blogSchema);
```

---

## Step 5: Signup API

```js
const bcrypt = require("bcryptjs");
const User = require("./models/User");

app.post("/api/signup", async (req, res) => {
  const { name, email, password } = req.body;

  const hashedPassword = await bcrypt.hash(password, 10);

  const user = new User({
    name,
    email,
    password: hashedPassword
  });

  await user.save();
  res.json({ message: "Signup successful" });
});
```

---

## Step 6: Login API with JWT

```js
const jwt = require("jsonwebtoken");

app.post("/api/login", async (req, res) => {
  const { email, password } = req.body;

  const user = await User.findOne({ email });
  if (!user) return res.status(400).json({ message: "User not found" });

  const isMatch = await bcrypt.compare(password, user.password);
  if (!isMatch) return res.status(400).json({ message: "Wrong password" });

  const token = jwt.sign(
    { userId: user._id },
    "SECRET_KEY",
    { expiresIn: "1h" }
  );

  res.json({ token });
});
```

---

## Step 7: Auth Middleware

### `middleware/auth.js`

```js
const jwt = require("jsonwebtoken");

module.exports = (req, res, next) => {
  const token = req.headers.authorization;

  if (!token) {
    return res.status(401).json({ message: "No token" });
  }

  const decoded = jwt.verify(token, "SECRET_KEY");
  req.userId = decoded.userId;
  next();
};
```

---

## Step 8: Create Blog API

```js
const Blog = require("./models/Blog");
const auth = require("./middleware/auth");

app.post("/api/blogs", auth, async (req, res) => {
  const blog = new Blog({
    title: req.body.title,
    content: req.body.content,
    userId: req.userId
  });

  await blog.save();
  res.json(blog);
});
```

---

## Step 9: Get All Blogs

```js
app.get("/api/blogs", async (req, res) => {
  const blogs = await Blog.find().populate("userId", "name");
  res.json(blogs);
});
```

---

## Step 10: Edit Blog

```js
app.put("/api/blogs/:id", auth, async (req, res) => {
  const blog = await Blog.findById(req.params.id);

  if (blog.userId.toString() !== req.userId) {
    return res.status(403).json({ message: "Not allowed" });
  }

  blog.title = req.body.title;
  blog.content = req.body.content;
  await blog.save();

  res.json(blog);
});
```

---

## Step 11: Delete Blog

```js
app.delete("/api/blogs/:id", auth, async (req, res) => {
  const blog = await Blog.findById(req.params.id);

  if (blog.userId.toString() !== req.userId) {
    return res.status(403).json({ message: "Not allowed" });
  }

  await blog.deleteOne();
  res.json({ message: "Blog deleted" });
});
```

---

# PART 3: FRONTEND IMPLEMENTATION

---

## Step 12: Frontend Setup

```bash
npm create vite@latest frontend
cd frontend
npm install axios react-router-dom
npm run dev
```

---

## Step 13: Signup Page

```jsx
import axios from "axios";
import { useState } from "react";

function Signup() {
  const [form, setForm] = useState({});

  const submit = async () => {
    await axios.post("http://localhost:5000/api/signup", form);
  };

  return (
    <>
      <input placeholder="Name" onChange={e => setForm({...form, name: e.target.value})} />
      <input placeholder="Email" onChange={e => setForm({...form, email: e.target.value})} />
      <input type="password" placeholder="Password" onChange={e => setForm({...form, password: e.target.value})} />
      <button onClick={submit}>Signup</button>
    </>
  );
}

export default Signup;
```

---

## Step 14: Login Page

```jsx
function Login() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  const login = async () => {
    const res = await axios.post("http://localhost:5000/api/login", {
      email,
      password
    });
    localStorage.setItem("token", res.data.token);
  };

  return (
    <>
      <input onChange={e => setEmail(e.target.value)} />
      <input type="password" onChange={e => setPassword(e.target.value)} />
      <button onClick={login}>Login</button>
    </>
  );
}
```

---

## Step 15: Create Blog Page

```jsx
function CreateBlog() {
  const [title, setTitle] = useState("");
  const [content, setContent] = useState("");

  const create = async () => {
    await axios.post("http://localhost:5000/api/blogs",
      { title, content },
      { headers: { Authorization: localStorage.getItem("token") } }
    );
  };

  return (
    <>
      <input onChange={e => setTitle(e.target.value)} />
      <textarea onChange={e => setContent(e.target.value)} />
      <button onClick={create}>Post</button>
    </>
  );
}
```

---

## Step 16: Display Blogs

```jsx
useEffect(() => {
  axios.get("http://localhost:5000/api/blogs")
    .then(res => setBlogs(res.data));
}, []);
```

---

## Step 17: Edit & Delete Blog (Concept)

- Show Edit/Delete only if logged-in user owns the blog
    
- Call PUT `/api/blogs/:id`
    
- Call DELETE `/api/blogs/:id`
    

---

# FINAL PROJECT FLOW

```
Signup → bcrypt → MongoDB
Login → bcrypt → JWT
JWT → Protected APIs
User → Create/Edit/Delete Blogs
Blogs → Stored in MongoDB
```

---

