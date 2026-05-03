# _01_ Prisma

Prisma is a next-generation ORM that makes working with databases easy with a clean API and strong type-safety.

## 🚀 Why use Prisma?
- **Type Safety:** Automatically generates a client based on your schema.
- **Prisma Schema:** A single source of truth for your database models.
- **Migrations:** Robust migration system that just works.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install prisma @prisma/client
npx prisma init
```

### Step 2: Schema Definition
Define your models in `prisma/schema.prisma`.

### Step 3: Client Generation
```bash
npx prisma generate
```

## 💻 Code Sample

```javascript
const { PrismaClient } = require('@prisma/client');
const express = require('express');

const prisma = new PrismaClient();
const app = express();
app.use(express.json());

// Create a User in MySQL/PostgreSQL via Prisma
app.post('/users', async (req, res) => {
  const { name, email } = req.body;
  const user = await prisma.user.create({
    data: { name, email },
  });
  res.json(user);
});

// Get all users
app.get('/users', async (req, res) => {
  const users = await prisma.user.findMany();
  res.json(users);
});

async function main() {
  // Connect the client
  await prisma.$connect();
  console.log('✅ Prisma Connected to Database');
}

main()
  .then(() => {
    app.listen(3000, () => console.log('🚀 Server ready at http://localhost:3000'));
  })
  .catch((e) => {
    console.error(e);
    process.exit(1);
  });
```
