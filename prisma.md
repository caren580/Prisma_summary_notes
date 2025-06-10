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

```bash
npx prisma init --datasource-provider DATABASE
```
Prisma uses postgresql by default, so if your database is postgresql, you can run the command without passing --datasource-provider flag.

```bash
npx prisma init
```

## Models
The data model definition part of the Prisma schema defines your application models (also called Prisma models). Models:
<ul>
<li>Represent the entities of your application domain</li>
<li>Map to the tables (relational databases like PostgreSQL) or collections (MongoDB) in your database</li>
<li>Form the foundation of the queries available in the generated Prisma Client API</li>
<li>When used with TypeScript, Prisma Client provides generated type definitions for your models and any variations of them to make database access entirely type safe.</li>
</ul>

```prisma
generator client {
 provider = "prisma-client-js"
}

datasource db {
 provider = "postgresql"
 url      = env("DATABASE_URL")
}

model User {
 id        Int       @id @default(autoincrement())
 email     String    @unique
 name      String?
 password  String
 createdAt DateTime  @default(now()) @map("created_at")
 updatedAt DateTime  @updatedAt @map("updated_at")
 posts     Post[]
 comments  Comment[]

 @@map("users")
}

model Post {
 id        Int       @id @default(autoincrement())
 title     String
 content   String?
 published Boolean   @default(false)
 createdAt DateTime  @default(now()) @map("created_at")
 updatedAt DateTime  @updatedAt @map("updated_at")
 authorId  Int       @map("author_id")
 author    User      @relation(fields: [authorId], references: [id], onDelete: Cascade)
 comments  Comment[]

 @@map("posts")
}

model Comment {
 id        Int      @id @default(autoincrement())
 content   String
 createdAt DateTime @default(now()) @map("created_at")
 updatedAt DateTime @updatedAt @map("updated_at")
 postId    Int      @map("post_id")
 post      Post     @relation(fields: [postId], references: [id], onDelete: Cascade)
 authorId  Int      @map("author_id")
 author    User     @relation(fields: [authorId], references: [id], onDelete: Cascade)

 @@map("comments")
}
```


#### Let's break down what's happening in this schema:

1. We've defined three models: User, Post, and Comment
2. Each model has fields with types like Int, String, Boolean, and DateTime
3. We're using attributes (prefixed with @) to define constraints and defaults
4. We've established relationships between models using the @relation attribute
5. We're using @@map to specify the actual table names in the database (following snake_case convention)

#### Some notable features in our schema include:
<ul>
<li>@id marks a field as the primary key</li>
<li>@default(autoincrement()) automatically increments the ID for new records</li>
<li>@unique ensures that the email field contains unique values</li>
<li>@updatedAt automatically updates the timestamp when a record changes</li>
<li>@map renames fields to follow database naming conventions</li>
</ul>

## Migrations
With our schema defined, it's time to create and apply migrations to set up our database tables. Prisma Migrate compares your schema to the current state of the database and generates the necessary SQL statements to synchronize them.
Run the following command to create your first migration:
```bash
npx prisma migrate dev --name MIGRATION-NAME
```
This command does three things:

1. Creates a new migration file in the prisma/migrations directory
2. Executes the SQL in that migration file against your database
3. Generates the Prisma Client based on your schema

## Prisma Client
The Prisma Client is an auto-generated and type-safe database client that you use to interact with your database in a Node.js or TypeScript application. It’s generated based on the models you define in your Prisma schema (schema.prisma) and provides a simple, intuitive, and type-safe API for CRUD operations, filtering, pagination, and more.
To generate a client, we use the command:
```bash
npx prisma generate
```
## Create a new user record
```
const user = await prisma.user.create({
  data: {
    email: 'elsa@gmail.com',
    name: 'Elsa Prisma',
  },
})
```
## Read
#### Get all record
The following findMany() query returns all User records:
```bash
const users = await prisma.user.findMany()
```
## Update
```bash
const updateUser = await prisma.user.update({
  where: {
    email: 'viola@prisma.io',
  },
  data: {
    name: 'Viola the Magnificent',
  },
})
```








