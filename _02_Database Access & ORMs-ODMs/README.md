# 2. Database Access & ORMs/ODMs

Managing data efficiently requires a balance between abstraction and control. Type-safety is non-negotiable in modern Node.js backends.

### **Prisma**
- **Why use it:** Type-safe database client with an incredible DX (Developer Experience). Auto-generated migrations and a visual studio make it a modern favorite.
- **Alternatives:** 
    - **TypeORM:** Great for OOP-style decorators.
    - **Sequelize:** The veteran SQL ORM (stable, battle-tested).
    - **Mongoose:** The de-facto standard for MongoDB.
    - **Knex.js:** A powerful SQL query builder for those who want more control than an ORM.
- **Use Case:** Modern TypeScript projects requiring strict type safety and rapid database schema evolution.
