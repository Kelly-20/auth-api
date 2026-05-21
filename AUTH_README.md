# Auth API

A RESTful Authentication API built with **NestJS**, **PostgreSQL**, **bcrypt**, and **JWT** — featuring secure user signup and login with hashed passwords and token-based authentication.

---

## Tech Stack

- **Runtime:** Node.js
- **Framework:** NestJS 11
- **Language:** TypeScript
- **Database:** PostgreSQL 16
- **ORM:** TypeORM
- **Authentication:** JWT (JSON Web Tokens)
- **Password Hashing:** bcrypt
- **Testing:** Postman

---

## Features

- User signup with hashed password storage
- User login with JWT token generation
- Password never stored as plain text
- Tokens expire after 1 day
- Duplicate email prevention

---

## Project Structure

```
src/
├── auth/
│   ├── auth.controller.ts       # Handles signup & login requests
│   ├── auth.service.ts          # Business logic, hashing & JWT
│   └── auth.module.ts           # Auth module registration
├── users/
│   ├── user.entity.ts           # PostgreSQL User table definition
│   ├── users.service.ts         # Database queries
│   └── users.module.ts          # Users module registration
├── app.module.ts                # Root module + DB connection
└── main.ts                      # Entry point (Port 3000)
```

---

## Getting Started

### Prerequisites
- Node.js (v18+)
- PostgreSQL 16
- npm

### Installation

```bash
# Clone the repository
git clone https://github.com/Kelly-20/auth-api.git

# Navigate into the project
cd auth-api

# Install dependencies
npm install
```

### Database Setup

1. Create a PostgreSQL database named `auth_db`
2. Update `src/app.module.ts` with your PostgreSQL credentials:

```typescript
TypeOrmModule.forRoot({
  type: 'postgres',
  host: 'localhost',
  port: 5432,
  username: 'postgres',
  password: 'your_password',
  database: 'auth_db',
  entities: [User],
  synchronize: true,
})
```

### Running the App

```bash
# Start development server
npm run start:dev
```

The server will start at **http://localhost:3000**

---

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/auth/signup` | Register a new user |
| POST | `/auth/login` | Login and receive JWT token |

---

## Example Usage

### Signup
```http
POST /auth/signup
Content-Type: application/json

{
  "email": "caleb@gmail.com",
  "password": "password123"
}
```

**Response:**
```json
{
  "message": "Signup successful",
  "userId": 1
}
```

---

### Login
```http
POST /auth/login
Content-Type: application/json

{
  "email": "caleb@gmail.com",
  "password": "password123"
}
```

**Response:**
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

---

### Error Responses

**Duplicate email on signup:**
```json
{
  "statusCode": 409,
  "message": "Email already in use"
}
```

**Wrong credentials on login:**
```json
{
  "statusCode": 401,
  "message": "Invalid credentials"
}
```

---

## Security Features

- Passwords hashed with **bcrypt** (10 salt rounds) — never stored as plain text
- JWT tokens signed with a secret key and expire after **1 day**
- Duplicate email check prevents multiple accounts with the same email

---

## What I Learned

Building this project taught me:
- Connecting NestJS to a real PostgreSQL database using TypeORM
- Defining database entities and letting TypeORM auto-create tables
- Securely hashing passwords with bcrypt
- Generating and signing JWT tokens for authentication
- Handling errors with NestJS built-in exceptions
- Structuring a real-world authentication system

---

## Author

**Caleb Kekeli**
- GitHub: [@Kelly-20](https://github.com/Kelly-20)

---

## Acknowledgement

Built as a portfolio project to demonstrate backend development skills while applying for the Backend Intern position at [codAfric](https://codafric.com) — a fast-growing African software startup building technology that fits the African context.
