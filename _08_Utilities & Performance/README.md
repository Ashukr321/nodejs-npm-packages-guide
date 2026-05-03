# 8. Utilities & Performance

Don't reinvent the wheel. Use battle-tested utilities for common tasks.

### **Lodash / Axios**
- **Why use it:** `Axios` is the standard for HTTP requests (automatic JSON parsing, interceptors). `Lodash` provides essential utility functions (though many are now native in modern Node.js).
- **Alternatives:** 
    - **Native Fetch:** Now built into Node.js (v18+).
    - **Got:** A powerful, human-friendly HTTP request library.
- **Use Case:** Data manipulation, fetching external API data, and handling complex object structures.
