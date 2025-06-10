# PRISMA
## What is Prisma?
Prisma ORM is a next-generation tool designed to simplify database interactions for Node.js and TypeScript applications. It offers a modern approach to database management, making it an attractive choice for developers seeking efficiency and reliability.
Prisma ORM is an open-source next-generation ORM. It consists of the following parts:
<ul>
<li>Prisma Client: Auto-generated and type-safe query builder for Node.js & TypeScript</li>

<li>Prisma Migrate: Migration system </li>

<li>Prisma Studio: GUI to view and edit data in your database.</li>
<ul>

## Benefits of using Prisma
#### Type Safety and Auto-Completion
One of the standout features of Prisma ORM is its emphasis on type safety. By generating type-safe queries, Prisma ensures that developers catch errors early in the development process. This not only improves code quality but also enhances developer productivity by reducing the time spent debugging.

#### Database Agnosticism
Prisma is designed to be database-agnostic, supporting multiple databases such as PostgreSQL, MySQL, SQL Server, SQLite, MongoDB, and CockroachDB. This flexibility allows developers to choose the best database for their specific use case without being locked into a single vendor.

#### Schema-Driven Development
1. Consistency: The schema file serves as a single source of truth for your data models, ensuring consistency across your application.
2. Automated Migrations: Prisma Migrate uses the schema file to generate and apply database migrations automatically. This simplifies the process of evolving your database schema and reduces the risk of migration errors.
3. Improved Collaboration: The schema file can be version-controlled, making it easier for teams to collaborate on database changes and track the history of schema modifications.

## Installation and Setup
### Installing Prisma CLI
The Prisma CLI is a powerful tool that helps you manage your Prisma project. To install it, run the following command:
```bash
npm install prisma -D
```
or
```bash
npm install prisma --save-dev
```
### Setting up a new prisma project
Once the Prisma CLI is installed, you can set up a new Prisma project. Start by initializing Prisma in your project directory:

``npx prisma init --datasource-provider DATABASE``



