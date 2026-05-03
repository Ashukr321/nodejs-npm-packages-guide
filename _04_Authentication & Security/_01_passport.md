# _01_ Passport.js

Passport is authentication middleware for Node.js. Extremely flexible and modular, Passport can be unobtrusively dropped into any Express-based web application.

## 🚀 Why use Passport?
- **Strategies:** Over 500+ authentication strategies (Google, Facebook, Twitter, JWT, etc.).
- **Unobtrusive:** Does not mount routes or assume any particular database schema.
- **Battle-tested:** The standard for Node.js authentication for years.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install passport passport-local express-session
```

### Step 2: Configuration
Configure your strategy (e.g., Local Strategy) and serialize/deserialize user sessions.

## 💻 Code Sample (Local Strategy)

```javascript
const express = require('express');
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;
const session = require('express-session');

const app = express();

// 1. Session Setup
app.use(session({ secret: 'secret', resave: false, saveUninitialized: false }));
app.use(passport.initialize());
app.use(passport.session());

// 2. Strategy Config
passport.use(new LocalStrategy(
  function(username, password, done) {
    // In a real app, verify against Database (Mongoose/MySQL)
    if (username === 'admin' && password === 'password') {
      return done(null, { id: 1, name: 'Admin' });
    }
    return done(null, false, { message: 'Incorrect credentials.' });
  }
));

passport.serializeUser((user, done) => done(null, user.id));
passport.deserializeUser((id, done) => done(null, { id: 1, name: 'Admin' }));

// 3. Routes
app.post('/login', 
  passport.authenticate('local', { failureRedirect: '/login' }),
  (req, res) => res.redirect('/dashboard')
);

app.listen(3000);
```
