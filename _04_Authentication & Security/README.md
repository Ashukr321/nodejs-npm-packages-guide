# 4. Authentication & Security

Security is not just a feature; it's a foundation. Proper handling of JWTs and multi-strategy auth is critical.

### **Passport.js / Jose**
- **Why use it:** `Passport` is the standard for multi-strategy auth (OAuth, Local, etc.). `Jose` is excellent for lightweight JWT (JSON Web Token) handling without heavy dependencies.
- **Alternatives:** 
    - **Lucia:** Modern, simple auth library that's becoming very popular for its simplicity.
    - **Auth0 / Clerk:** External managed solutions for enterprise-grade security.
    - **Helmet:** Middleware for setting various HTTP headers to secure your app.
- **Use Case:** Implementing login systems, social auth, and securing API endpoints.
