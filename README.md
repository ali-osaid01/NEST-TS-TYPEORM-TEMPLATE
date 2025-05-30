<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>NestJS + TypeORM + PostgreSQL Template</title>
</head>
<body>

  <h1>🚀 NestJS + TypeORM + PostgreSQL Starter Template</h1>
  <p>A <strong>production-ready NestJS boilerplate</strong> integrated with <strong>TypeORM</strong> and <strong>PostgreSQL</strong>. This template helps you quickly build scalable server-side applications with a clean architecture.</p>

  <h2>Getting Started</h2>

  <h3>1️⃣ Clone the Repository</h3>
  <pre><code>git clone https://github.com/your-username/nestjs-typeorm-postgres-template.git
cd nestjs-typeorm-postgres-template
  </code></pre>

  <h3>2️⃣ Install Dependencies</h3>
  <pre><code>npm install</code></pre>

  <h3>3️⃣ Configure Environment Variables</h3>
  <p>Create a <code>.env</code> file at the root of the project:</p>
  <pre><code>DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_USER=postgres
DATABASE_PASSWORD=yourpassword
DATABASE_NAME=nestjs_db

PORT=3000
  </code></pre>

  <h3>4️⃣ Run the Application</h3>

  <p><strong>Development Mode (with Hot Reload)</strong></p>
  <pre><code>npm run start:dev</code></pre>

  <p><strong>Production Mode</strong></p>
  <pre><code>npm run build
npm run start:prod</code></pre>

  <h2>TypeORM in This Project</h2>

  <h3>1️⃣ Entities (Models)</h3>
  <pre><code>// src/entities/user.entity.ts
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
  </code></pre>

  <h3>2️⃣ Repositories and Services</h3>
  <pre><code>// src/user/user.service.ts
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

  async findAll(): Promise&lt;User[]&gt; {
    return this.userRepository.find();
  }

  async create(data: Partial&lt;User&gt;): Promise&lt;User&gt; {
    const user = this.userRepository.create(data);
    return this.userRepository.save(user);
  }
}
  </code></pre>

  <h3>3️⃣ Migrations</h3>
  <ul>
    <li><strong>Create a Migration</strong>
      <pre><code>npm run typeorm migration:generate -- -n CreateUserTable</code></pre>
    </li>
    <li><strong>Run Migrations</strong>
      <pre><code>npm run typeorm migration:run</code></pre>
    </li>
    <li><strong>Revert Migrations</strong>
      <pre><code>npm run typeorm migration:revert</code></pre>
    </li>
  </ul>

  <h2>🏗️ Project Structure</h2>
  <pre><code>src/
├── entities/          # TypeORM entities (database models)
├── user/              # Example feature module
│   ├── user.controller.ts
│   ├── user.module.ts
│   └── user.service.ts
├── app.module.ts      # Main app module
├── main.ts            # Application entry point
  </code></pre>

  <h2>🛠️ Useful Commands</h2>
  <table border="1" cellpadding="5" cellspacing="0">
    <tr>
      <th>Command</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>npm run start:dev</code></td>
      <td>Run in development mode (hot reload)</td>
    </tr>
    <tr>
      <td><code>npm run start:prod</code></td>
      <td>Run in production mode</td>
    </tr>
    <tr>
      <td><code>npm run typeorm migration:generate -- -n Name</code></td>
      <td>Create a new migration</td>
    </tr>
    <tr>
      <td><code>npm run typeorm migration:run</code></td>
      <td>Run pending migrations</td>
    </tr>
    <tr>
      <td><code>npm run typeorm migration:revert</code></td>
      <td>Rollback last migration</td>
    </tr>
  </table>

  <h2>🌟 Contribution</h2>
  <p>Feel free to fork this repo, add features, and submit pull requests! 💪</p>

  <h2>📄 License</h2>
  <p>MIT</p>

</body>
</html>
