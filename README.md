# Task Management REST API

This project implements a RESTful API for a simple Task Management System, allowing users to manage tasks with standard CRUD operations.

## Table of Contents

* [Features](#features)
* [Technologies Used](#technologies-used)
* [API Endpoints](#api-endpoints)
    * [User Management](#user-management)
    * [Task Management](#task-management)
* [Functional Requirements Implemented](#functional-requirements-implemented)
* [Getting Started](#getting-started)
    * [Prerequisites](#prerequisites)
    * [Installation](#installation)
    * [Running the Application](#running-the-application)
* [Database Schema](#database-schema)
* [Authentication & Authorization](#authentication--authorization)
* [Error Handling](#error-handling)
* [API Documentation](#api-documentation)
* [Code Quality](#code-quality)
* [Deployment (Optional)](#deployment-optional)
* [Submission Details](#submission-details)

## Features

* [cite_start]**User Management:** Register, retrieve, and update user information. [cite: 7, 8]
* [cite_start]**Task Management:** Create, list, retrieve, update, and delete tasks. [cite: 9, 10]
* [cite_start]**Authentication & Authorization:** Secure endpoints using JWT. 
* [cite_start]**Data Validation:** Validate input data for all requests. [cite: 15, 16]
* [cite_start]**Error Handling:** Graceful error handling with appropriate HTTP status codes. 
* [cite_start]**Database Integration:** Persistence of user and task data. [cite: 18, 20, 21]

## Technologies Used

* [cite_start]**Backend:** Node.js (preferred as per requirements) [cite: 5]
* **Web Framework:** Express.js
* [cite_start]**Database:** [Choose one: e.g., MongoDB (for NoSQL) or PostgreSQL/MySQL (for SQL)] [cite: 20]
* **ORM/ODM:** [If using SQL: Sequelize, TypeORM, Prisma; [cite_start]If using NoSQL: Mongoose] [cite: 29]
* **Authentication:** `jsonwebtoken`, `bcrypt` (for password hashing)
* **Validation:** `express-validator` or Joi
* **Environment Variables:** `dotenv`

## API Endpoints

### [cite_start]User Management [cite: 7]

| Endpoint            | Method | Description                                    | Access                     |
| :------------------ | :----- | :--------------------------------------------- | :------------------------- |
| `/users`            | POST   | Register a new user (name, email, password).   | Public                     |
| `/users`            | GET    | Get a list of all users.                       | [cite_start]Private (Any logged-in user) [cite: 8] |
| `/users/{userId}`   | GET    | Get details of a specific user.                | [cite_start]Private (Any logged-in user) [cite: 8] |
| `/users/{userId}`   | PUT    | Update a user's information (name, email).     | [cite_start]Private (Any logged-in user) [cite: 8] |

### [cite_start]Task Management [cite: 9]

| Endpoint            | Method   | Description                                            | Access   |
| :------------------ | :------- | :----------------------------------------------------- | :------- |
| `/tasks`            | POST     | Create a new task (title, description, due date, assigned user). | Private  |
| `/tasks`            | GET      | List all tasks (task id, title).                       | Private  |
| `/tasks/{taskId}`   | GET      | Retrieve a specific task by ID.                        | Private  |
| `/tasks/{taskId}`   | PUT      | Update a task (title, description, status, due date).  | Private  |
| `/tasks/{taskId}`   | DELETE   | Delete a task by ID.                                   | Private  |

## Functional Requirements Implemented

* [cite_start]**Authentication & Authorization:** JWT is used for securing private endpoints. 
* [cite_start]**Data Validation & Error Handling:** Input data is validated, and errors are handled with appropriate HTTP status codes (e.g., 400, 404, 500). [cite: 15, 16, 17]
* **Database:** [Specify chosen database, e.g., MongoDB/PostgreSQL] is used for data persistence. [cite_start]Schemas are designed for efficient querying. [cite: 18, 20, 21]
* [cite_start]**Documentation:** This README serves as primary API documentation, detailing endpoints, request/response formats, and error responses. [cite: 22, 23, 25]
* [cite_start]**Code Quality:** The codebase follows best practices for clean, maintainable, and modular code. 

## Getting Started

### Prerequisites

* Node.js (LTS version recommended)
* npm or yarn
* [Chosen Database] (e.g., MongoDB, PostgreSQL)

### Installation

1.  Clone the repository:
    ```bash
    git clone <your-repository-link>
    cd <project-directory>
    ```
2.  Install dependencies:
    ```bash
    npm install
    # or
    yarn install
    ```
3.  Create a `.env` file in the root directory and add your environment variables:

    ```
    PORT=3000
    MONGO_URI=your_mongodb_connection_string
    JWT_SECRET=your_jwt_secret_key
    # Or for SQL:
    # DB_HOST=localhost
    # DB_PORT=5432
    # DB_USER=your_user
    # DB_PASSWORD=your_password
    # DB_NAME=your_database_name
    ```

### Running the Application

1.  Start the server:
    ```bash
    npm start
    # or
    yarn start
    ```
    The API will be running at `http://localhost:PORT`.

## Database Schema

### User Schema

* `_id` (or `id`): Primary Key (UUID/ObjectID)
* `name`: String, required
* `email`: String, required, unique, valid email format
* `password`: String, required (hashed)
* `createdAt`: Date (timestamp)
* `updatedAt`: Date (timestamp)

[cite_start]**SQL Example (`users` table):** 

```sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);