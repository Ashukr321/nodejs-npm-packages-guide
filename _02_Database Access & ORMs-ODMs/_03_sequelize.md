# _03_ Sequelize

Sequelize is a modern TypeScript and Node.js ORM for Oracle, Postgres, MySQL, MariaDB, SQLite and SQL Server, and more.

## 🚀 Why use Sequelize?
- **Promise-based:** Native support for async/await.
- **Migrations:** Built-in CLI for managing database schema changes.
- **Relations:** Easy handling of One-to-One, One-to-Many, and Many-to-Many relationships.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install sequelize mysql2
```

### Step 2: Instance Setup
Create a Sequelize instance and define your connection.

## 💻 Code Sample

```javascript
const { Sequelize, DataTypes } = require('sequelize');

// 1. Connection
const sequelize = new Sequelize('database', 'username', 'password', {
  host: 'localhost',
  dialect: 'mysql'
});

// 2. Model Definition
const User = sequelize.define('User', {
  username: {
    type: DataTypes.STRING,
    allowNull: false
  },
  birthday: DataTypes.DATE
});

// 3. Sync and Usage
async function init() {
  await sequelize.authenticate();
  console.log('✅ Connection has been established successfully.');
  
  await sequelize.sync({ force: true }); // Sync models to DB
  
  const jane = await User.create({
    username: 'janedoe',
    birthday: new Date(1980, 6, 20)
  });
  
  console.log('Jane saved:', jane.toJSON());
}

init().catch(err => console.error('Unable to connect to the database:', err));
```
