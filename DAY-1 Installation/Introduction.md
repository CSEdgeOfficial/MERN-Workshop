
# Day 1: Understanding Web Applications & MongoDB Setup (6 Hours)

---

##  Learning Goals

By the end of Day 1, you will:

- Understand how web applications work
    
- Know what **MERN Stack** is and how its parts connect
    
- Create and explore a **MongoDB Atlas** database
    
- Use **MongoDB Compass** for visual data handling
    
- Set up **React (Vite)** and **Node.js**
    
- Run your first **Hello World** app in React and Node
    

---

## 1. How the Web Works 

###  Main Components

A web application usually has **three parts**:

```
Client (Browser) → Server → Database
```

### 🔹 Client

- Runs in the browser (Chrome, Firefox)
    
- Built with **HTML, CSS, JavaScript**
    
- In MERN → **React**
    
### 🔹 Server

- Handles requests and responses
    
- Business logic (login, validation)
    
- In MERN → **Node.js + Express**
    
### 🔹 Database

- Stores data (users, posts, products)
    
- In MERN → **MongoDB**
    

---

## 2. What is MERN Stack?

**MERN** stands for:

|Letter|Technology|Role|
|---|---|---|
|M|MongoDB|Database|
|E|Express.js|Backend framework|
|R|React|Frontend library|
|N|Node.js|JavaScript runtime|

📌 **Why MERN?**

- One language: **JavaScript everywhere**
    
- Fast development
    
- Popular in real-world projects
    

---

## 3 Creating a MongoDB Atlas Account 

### Steps:

1. Go to 👉 [https://www.mongodb.com/atlas](https://www.mongodb.com/atlas)
    
2. Sign up (Google / Email)
    
3. Create a **Free Shared Cluster**
    
4. Choose:
    
    - Provider: AWS
        
    - Region: Nearest to you
        
5. Create a database user (username + password)
    
6. Whitelist IP: `0.0.0.0/0` (for development)
    

---

## 4. Exploring MongoDB Atlas Dashboard

### Key Sections:

- **Clusters** → Your database server
    
- **Database** → Collections & documents
    
- **Network Access** → IP settings
    
- **Security** → Users & roles
    

---

## 5. Creating Databases & Collections

### Example:

- Database name: `mern_app`
    
- Collection name: `users`
    

### Sample Document (JSON)

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "age": 22,
  "isActive": true
}
```

 MongoDB stores data in **documents** (JSON-like format).

---

## 6. Using MongoDB Compass 

### What is MongoDB Compass?

A **GUI tool** to visually manage MongoDB.

### Steps:

1. Download MongoDB Compass
    
2. Copy connection string from Atlas
    
3. Paste into Compass
    
4. Connect
    

### You can:

- Add documents
    
- Edit fields
    
- Delete records
    
- Run queries visually
    

---

## 7. Simple Data Planning for an App 

Before coding, plan your data.

### Example: User Collection

```js
User {
  name: String
  email: String
  password: String
  createdAt: Date
}
```

 Good planning avoids bugs later.

---

## 8. Installing Required Tools 

### Node.js

- Download from: [https://nodejs.org](https://nodejs.org/)
    
- Check installation:
    

```bash
node -v
npm -v
```

### VS Code

- Download from: [https://code.visualstudio.com](https://code.visualstudio.com/)

### Recommended Extensions:

- ES7+ React Snippets

---

## 9. Setting Up React with Vite 

### Create React App

```bash
npm create vite@latest my-react-app
cd my-react-app
npm install
npm run dev
```

### Project Structure

```
src/
 ├─ App.jsx
 ├─ main.jsx
 └─ index.css
```

---

## 10. React Hello World 👋

### `App.jsx`

```jsx
function App() {
  return (
    <h1>Hello World from React 🚀</h1>
  );
}

export default App;
```

---

## 11. Node.js Hello World 

### Create a file: `server.js`

```js
const http = require("http");

const server = http.createServer((req, res) => {
  res.end("Hello World from Node.js");
});

server.listen(5000, () => {
  console.log("Server running on port 5000");
});
```

### Run Server

```bash
node server.js
```

Open browser:  
👉 `http://localhost:5000`
