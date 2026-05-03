# _03_ NestJS

Nest (NestJS) is a framework for building efficient, scalable Node.js server-side applications. It uses progressive JavaScript and is built with and fully supports TypeScript.

## 🚀 Why use NestJS?
- **Architecture:** Heavily inspired by Angular; provides a clear structure (Modules, Controllers, Services).
- **Enterprise Ready:** Built-in support for Microservices, WebSockets, GraphQL, and more.
- **Dependency Injection:** Powerful DI system for maintainable and testable code.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install @nestjs/common @nestjs/core @nestjs/mongoose mongoose @nestjs/typeorm typeorm mysql2
```

### Step 2: Module Configuration
Import `MongooseModule` and `TypeOrmModule` into your `AppModule`.

## 💻 Code Sample (Conceptual)

```typescript
// app.module.ts
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';
import { TypeOrmModule } from '@nestjs/typeorm';

@Module({
  imports: [
    // --- 1. Mongoose Integration ---
    MongooseModule.forRoot('mongodb://localhost/nest'),
    
    // --- 2. MySQL Integration (via TypeORM) ---
    TypeOrmModule.forRoot({
      type: 'mysql',
      host: 'localhost',
      port: 3306,
      username: 'root',
      password: 'password',
      database: 'test',
      autoLoadEntities: true,
      synchronize: true,
    }),
  ],
})
export class AppModule {}

// user.service.ts
import { Injectable } from '@nestjs/common';
import { InjectModel } from '@nestjs/mongoose';
import { Model } from 'mongoose';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { UserEntity } from './user.entity';

@Injectable()
export class UserService {
  constructor(
    @InjectModel('User') private mongoUserModel: Model<any>,
    @InjectRepository(UserEntity) private mysqlUserRepository: Repository<UserEntity>,
  ) {}

  async findAll() {
    const mongoUsers = await this.mongoUserModel.find().exec();
    const mysqlUsers = await this.mysqlUserRepository.find();
    return { mongoUsers, mysqlUsers };
  }
}
```
