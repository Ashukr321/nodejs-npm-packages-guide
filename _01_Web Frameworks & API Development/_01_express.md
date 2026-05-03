# _01_ Express.js

Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications.

## 🚀 Why use Express?
- **Ubiquity:** Most documented and widely used framework.
- **Middleware:** Thousands of pre-built middlewares (auth, logging, parsing).
- **Flexibility:** Unopinionated, allowing you to structure your app however you like.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install express mongoose mysql2
```

### Step 2: Basic Server Setup
Create an `app.js` or `server.js` and initialize Express.

### Step 3: Connect to Databases
Configure your connection strings and handle the connection logic.

## 💻 Code Sample

```javascript
const express = require('express');
const mongoose = require('mongoose');
const mysql = require('mysql2/promise');

const app = express();
app.use(express.json());

// --- 1. Mongoose (MongoDB) Integration ---
mongoose.connect('mongodb://localhost:27017/my_database')
  .then(() => console.log('✅ MongoDB Connected'))
  .catch(err => console.error('❌ MongoDB Connection Error:', err));

const UserSchema = new mongoose.Schema({ name: String, email: String });
const User = mongoose.model('User', UserSchema);

// --- 2. MySQL Integration ---
const mysqlPool = mysql.createPool({
  host: 'localhost',
  user: 'root',
  password: 'password',
  database: 'test_db'
});

// --- API Routes ---

// Get Users from MongoDB
app.get('/mongo-users', async (req, res) => {
  const users = await User.find();
  res.json(users);
});

// Get Users from MySQL
app.get('/mysql-users', async (req, res) => {
  try {
    const [rows] = await mysqlPool.query('SELECT * FROM users');
    res.json(rows);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`🚀 Server running on http://localhost:${PORT}`);
});
```
