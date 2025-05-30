NestJS + TypeORM + PostgreSQL Starter Template
A production-ready NestJS boilerplate integrated with TypeORM and PostgreSQL. This template helps you quickly build scalable server-side applications with a clean architecture.

🚀 Getting Started
1️⃣ Clone the Repository
bash
Copy
Edit
git clone https://github.com/your-username/nestjs-typeorm-postgres-template.git
cd nestjs-typeorm-postgres-template
2️⃣ Install Dependencies
bash
Copy
Edit
npm install
3️⃣ Configure Environment Variables
Create a .env file at the root of the project and add your database configuration:

bash
Copy
Edit
# .env
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_USER=postgres
DATABASE_PASSWORD=yourpassword
DATABASE_NAME=nestjs_db

# Other configurations
PORT=3000
4️⃣ Run the Application
Development Mode (with Hot Reload)
bash
Copy
Edit
npm run start:dev
Production Mode
bash
Copy
Edit
npm run build
npm run start:prod
🔗 TypeORM in This Project
This template uses TypeORM as the ORM for database operations. Here's how to work with it:

1️⃣ Entities (Models)
Entities are defined in the src/entities folder. For example:

typescript
Copy
Edit
// src/entities/user.entity.ts
import { Entity, PrimaryGeneratedColumn, Column } from 'typeorm';

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  @Column()
  email: string;
}
2️⃣ Repositories and Services
Use TypeORM's Repository in your services:

typescript
Copy
Edit
// src/user/user.service.ts
import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { User } from '../entities/user.entity';

@Injectable()
export class UserService {
  constructor(
    @InjectRepository(User)
    private userRepository: Repository<User>,
  ) {}

  async findAll(): Promise<User[]> {
    return this.userRepository.find();
  }

  async create(data: Partial<User>): Promise<User> {
    const user = this.userRepository.create(data);
    return this.userRepository.save(user);
  }
}
3️⃣ Migrations
To handle database migrations:

Create a Migration
bash
Copy
Edit
npm run typeorm migration:generate -- -n CreateUserTable
Run Migrations
bash
Copy
Edit
npm run typeorm migration:run
Revert Migrations
bash
Copy
Edit
npm run typeorm migration:revert
Migration configurations are in ormconfig.js.

🏗️ Project Structure
ruby
Copy
Edit
src/
├── entities/          # TypeORM entities (database models)
├── user/              # Example feature module
│   ├── user.controller.ts
│   ├── user.module.ts
│   └── user.service.ts
├── app.module.ts      # Main app module
├── main.ts            # Application entry point
🛠️ Useful Commands
Command	Description
npm run start:dev	Run in development mode (hot reload)
npm run start:prod	Run in production mode
npm run typeorm migration:generate -- -n Name	Create a new migration
npm run typeorm migration:run	Run pending migrations
npm run typeorm migration:revert	Rollback last migration

🌟 Contribution
Feel free to fork this repo, add features, and submit pull requests! 💪

📄 License
MIT

