# _01_ Dotenv

Dotenv is a zero-dependency module that loads environment variables from a `.env` file into `process.env`.

## 🚀 Why use Dotenv?
- **Security:** Keeps sensitive keys (API secrets, DB passwords) out of your source code.
- **Portability:** Easily switch between Dev, Staging, and Production configs by changing the `.env` file.
- **Simplicity:** Extremely easy to set up and use.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install dotenv
```

### Step 2: Initialize
Call `require('dotenv').config()` at the very top of your entry file.

## 💻 Code Sample

> [!CAUTION]
> **NEVER** commit your `.env` file to version control. Add it to your `.gitignore` immediately to prevent leaking sensitive credentials.

```javascript
// 1. Load variables at the earliest possible point
require('dotenv').config();

// 2. Access variables via process.env
const dbUrl = process.env.DATABASE_URL;
const port = process.env.PORT || 3000;

console.log(`Server will run on port: ${port}`);

// Example .env file content:
/*
PORT=5000
DATABASE_URL=mongodb://localhost:27017/mydb
API_KEY=your_secret_api_key_here
*/
```
