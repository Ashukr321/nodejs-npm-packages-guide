# _02_ Fastify

Fastify is a web framework highly focused on providing the best developer experience with the least overhead and a powerful plugin architecture.

## 🚀 Why use Fastify?
- **Performance:** 2x-3x faster than Express in most benchmarks.
- **Schema Validation:** Built-in JSON Schema validation for inputs/outputs.
- **Developer Experience:** Modern, async/await first, and excellent TypeScript support.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install fastify mongoose mysql2
```

### Step 2: Basic Server Setup
Fastify uses a plugin system for everything, including database connections.

## 💻 Code Sample

```javascript
const fastify = require('fastify')({ logger: true });
const mongoose = require('mongoose');
const mysql = require('mysql2/promise');

// --- 1. Mongoose Integration ---
const connectDB = async () => {
  try {
    await mongoose.connect('mongodb://localhost:27017/fastify_db');
    fastify.log.info('✅ MongoDB Connected');
  } catch (err) {
    fastify.log.error(err);
    process.exit(1);
  }
};

const User = mongoose.model('User', new mongoose.Schema({ name: String }));

// --- 2. MySQL Integration (as a decorator) ---
fastify.decorate('mysql', mysql.createPool({
  host: 'localhost',
  user: 'root',
  database: 'test'
}));

// --- Routes ---

fastify.get('/users', async (request, reply) => {
  // Fetch from Mongo
  const mongoUsers = await User.find();
  
  // Fetch from MySQL
  const [mysqlRows] = await fastify.mysql.query('SELECT * FROM users');
  
  return { mongoUsers, mysqlRows };
});

const start = async () => {
  await connectDB();
  try {
    await fastify.listen({ port: 3000 });
  } catch (err) {
    fastify.log.error(err);
    process.exit(1);
  }
};

start();
```
