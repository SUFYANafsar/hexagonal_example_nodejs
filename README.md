# Hexagonal Architecture example in Node.js using TypeScript
This is a simple example of Hexagonal Architecture in Node.js using TypeScript.
I made this example to show how to implement the Hexagonal Architecture in Node.js using TypeScript with my underestanding of the concept.

## What is Hexagonal Architecture?
Hexagonal Architecture is an architectural pattern that helps us to create applications that are more independent of the external world.
It is also known as Ports and Adapters Architecture or Onion Architecture.

## Project Folder Structure
rc/
│
├── adapter/                # Adapters (Ports implementations)
│   ├── primary/            # Input adapters (driving) e.g. Controllers
│   │   ├── post/
│   │   │   └── PostCreateController.ts
│   │   └── user/
│   │       ├── AuthUserController.ts
│   │       └── UserCreateController.ts
│   │
│   ├── secondary/          # Output adapters (driven) e.g. DB, Events
│   │   ├── events/
│   │   │   ├── BaseEventHandler.ts
│   │   │   └── PostEventHandler.ts
│   │   ├── post/
│   │   │   └── PostRepository.ts
│   │   └── user/
│   │       └── UserRepository.ts (example)
│   │
│   ├── PostMapper.ts
│   └── UserMapper.ts
│
├── application/            # Application layer (use cases, services)
│   ├── helpers/
│   │   ├── jwt_utility.ts
│   │   └── password_utility.ts
│   │
│   ├── Post/
│   │   ├── domain/
│   │   │   ├── IPost.ts
│   │   │   ├── Post.ts
│   │   │   └── PostEvent.ts
│   │   ├── port/
│   │   │   ├── primary/
│   │   │   └── secondary/
│   │   └── usecases/
│   │       ├── CreatePost.ts
│   │       └── GetPost.ts
│   │
│   └── User/
│       ├── domain/
│       ├── port/
│       │   ├── primary/
│       │   └── secondary/
│       └── usecases/
│           ├── CreateUser.ts
│           └── AuthenticateUser.ts
│
├── infrastructure/         # Infrastructure (DB, framework specifics)
│   └── db/
│       ├── prisma.schema
│       └── migrations/
│
├── lib/                    # Shared utilities
│   ├── Event.ts
│   ├── DIContainer.ts
│   └── logger.ts
│
├── Errors/                 # Domain/application errors
│
├── UI/                     # Entry points (e.g. Express, GraphQL, CLI)
│
├── tests/                  # Tests (unit, integration)
│   ├── fakes/
│   ├── post/
│   └── user/
│
└── index.ts                # App entrypoint


## Explanation

adapter/: Implements the ports (both primary = controllers, and secondary = persistence/events).

application/: Use cases (business logic orchestrators) + domain models + ports.

infrastructure/: Tech details like Prisma, DB migrations, external APIs.

lib/: Shared libraries (DI container, events, logging).

Errors/: Centralized error definitions.

UI/: Entry point for framework-specific setup (Express, Fastify, CLI, etc).

tests/: Unit & integration tests with fakes/mocks.

## How to run the application

pre-requisites:

- Node.js
- npm
- prisma => `npm install -g prisma`


1. Clone the repository


2. Run `npm install`


3. cd into the `src/infrastructure/db` folder 
```
cd src/infrastructure/db

npx prisma migrate dev --name init
```


4. Run `npm run start` to start the application


5. Run `npm run test` to run the tests


## usecases
this is the list of the usecases that the application supports,this usecases will be changed in the future to be more realistic.
### Create user
I want to create a user with the following data:

- name
- email
- password

```json
{
  "name": "John Doe",
  "email": "john@test.com",
  "password": "123456"
}
  
  ```
### Authenticate user
I want to authenticate a user with the following data:

- email
- password

```json
{
  "email": "john@test.com",
    "password": "123456"
}
    
```
### Create post
I want to create a post with the following data:

- title
- content

```json
{
  "title": "My first post",
  "content": "This is my first post",
}
    
```
