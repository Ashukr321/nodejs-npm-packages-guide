# _01_ Jest

Jest is a delightful JavaScript Testing Framework with a focus on simplicity.

## 🚀 Why use Jest?
- **Zero Config:** Works out of the box for most projects.
- **Snapshots:** Powerful tool for ensuring UI or large data structures don't change unexpectedly.
- **Mocks:** Built-in mocking for functions, modules, and timers.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install --save-dev jest supertest
```

### Step 2: Configuration
Add a test script to `package.json`: `"test": "jest"`.

## 💻 Code Sample (Testing an Express API)

```javascript
// app.js
const express = require('express');
const app = express();
app.get('/user', (req, res) => res.status(200).json({ name: 'john' }));
module.exports = app;

// app.test.js
const request = require('supertest');
const app = require('./app');

describe('GET /user', () => {
  it('should respond with json containing the user name', async () => {
    const response = await request(app)
      .get('/user')
      .set('Accept', 'application/json');
    
    expect(response.status).toBe(200);
    expect(response.body.name).toBe('john');
  });
});
```
