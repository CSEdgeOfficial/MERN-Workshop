```jsx
const express = require("express");
const app = express();
const mongoose = require("mongoose");

app.use(express.json());

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  password: String,
});

const User = mongoose.model("User", userSchema);

app.get("/", async (req, res) => {
  const users = await User.find();
  res.json(users);
});

app.post("/", async (req, res) => {
  const userDetails = req.body;
  const createdUser = await User.create(userDetails);
  res.json({
    message: "user has been created",
  });
});

app.put("/", (req, res) => {});

app.delete("/", (req, res) => {});

app.listen(5000, () => {
  mongoose
    .connect("mongodb://admin:secret@localhost:27017/")
    .then(() => {
      console.log("MongoDB is successfully connected");
    })
    .catch((err) => {
      console.log(err);
    });
  console.log("Server is running on port 5000");
});

```