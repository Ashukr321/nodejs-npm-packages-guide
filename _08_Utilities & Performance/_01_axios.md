# _01_ Axios

Axios is a promise-based HTTP client for the browser and node.js.

## 🚀 Why use Axios?
- **Interceptors:** Intercept requests or responses before they are handled by `then` or `catch`.
- **Auto JSON:** Automatic transformation of JSON data.
- **Node.js Support:** Robust support for handling streams and buffers in a Node environment.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install axios
```

### Step 2: Instance Configuration
Create a base instance with common headers and timeouts.

## 💻 Code Sample

```javascript
const axios = require('axios');

// 1. Create Instance
const api = axios.create({
  baseURL: 'https://api.example.com',
  timeout: 5000,
  headers: { 'X-Custom-Header': 'foobar' }
});

// 2. Add Interceptor
api.interceptors.request.use(config => {
  const token = 'my-auth-token';
  config.headers.Authorization = `Bearer ${token}`;
  return config;
});

// 3. Usage
async function getUser() {
  try {
    const response = await api.get('/user/123');
    console.log(response.data);
  } catch (error) {
    console.error('API Error:', error.message);
  }
}
```
