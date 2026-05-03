# _01_ Zod

Zod is a TypeScript-first schema declaration and validation library.

## 🚀 Why use Zod?
- **Zero Dependencies:** Tiny footprint.
- **TypeScript First:** Automatically infers types from your schema.
- **Developer Experience:** Concise and intuitive API.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install zod
```

### Step 2: Schema Definition
Create a schema that matches your expected data structure.

## 💻 Code Sample

```javascript
const { z } = require('zod');
const express = require('express');
const app = express();
app.use(express.json());

// 1. Define Schema
const UserSchema = z.object({
  username: z.string().min(3).max(20),
  email: z.string().email(),
  age: z.number().min(18).optional()
});

// 2. Validation Middleware
const validate = (schema) => (req, res, next) => {
  try {
    schema.parse(req.body);
    next();
  } catch (err) {
    return res.status(400).json({ errors: err.errors });
  }
};

// 3. Usage
app.post('/register', validate(UserSchema), (req, res) => {
  res.json({ message: 'Success', data: req.body });
});

app.listen(3000);
```
