# _01_ Winston

Winston is designed to be a simple and universal logging library with support for multiple transports.

## 🚀 Why use Winston?
- **Transports:** Log to console, file, HTTP, or even databases like MongoDB.
- **Formats:** Custom formats (JSON, simple text, timestamps).
- **Log Levels:** Standard RFC5424 levels (error, warn, info, debug).

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install winston
```

### Step 2: Logger Configuration
Create a logger instance with desired transports and levels.

## 💻 Code Sample

```javascript
const winston = require('winston');

// 1. Create Logger
const logger = winston.createLogger({
  level: 'info',
  format: winston.format.combine(
    winston.format.timestamp(),
    winston.format.json()
  ),
  transports: [
    new winston.transports.Console(),
    new winston.transports.File({ filename: 'error.log', level: 'error' }),
    new winston.transports.File({ filename: 'combined.log' })
  ],
});

// 2. Integration with Express
const express = require('express');
const app = express();

app.use((req, res, next) => {
  logger.info(`${req.method} ${req.url}`);
  next();
});

app.get('/', (req, res) => {
  res.send('Hello World');
});

app.get('/error', (req, res) => {
  try {
    throw new Error('Something went wrong!');
  } catch (err) {
    logger.error(err.message);
    res.status(500).send('Error logged');
  }
});

app.listen(3000, () => logger.info('🚀 Server started on port 3000'));
```
