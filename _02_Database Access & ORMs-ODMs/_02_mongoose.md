# _02_ Mongoose

Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It manages relationships between data, provides schema validation, and is used to translate between objects in code and the representation of those objects in MongoDB.

## 🚀 Why use Mongoose?
- **Schemas:** Enforces a structure on top of MongoDB's schemaless nature.
- **Validation:** Built-in and custom validation rules.
- **Middleware:** Pre and post hooks for save, delete, etc.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install mongoose
```

### Step 2: Connection
Connect to your MongoDB instance using a URI.

## 💻 Code Sample

```javascript
const mongoose = require('mongoose');

// 1. Connection
mongoose.connect('mongodb://localhost:27017/myapp')
  .then(() => console.log('✅ Connected to MongoDB'))
  .catch(err => console.error('❌ Connection error', err));

// 2. Schema Definition
const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, unique: true },
  createdAt: { type: Date, default: Date.now }
});

// 3. Model Creation
const User = mongoose.model('User', userSchema);

// 4. Usage in Express
const express = require('express');
const app = express();
app.use(express.json());

app.post('/users', async (req, res) => {
  try {
    const user = new User(req.body);
    await user.save();
    res.status(201).json(user);
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
});

app.listen(3000, () => console.log('🚀 Server running on port 3000'));
```
