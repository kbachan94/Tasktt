# Tasktt – Architecture Overview

## Overview
Tasktt is a task management application that allows users to
register, authenticate, and manage personal tasks securely.

The application follows a client-server architecture using a RESTful API
and a relational database.

---

## High-Level Architecture
- Frontend: React
- Backend: Node.js with Express
- Database: PostgreSQL
- Authentication: JWT-based authentication

---

## Client
The client is a React application responsible for:
- Rendering the user interface
- Handling user input
- Managing authentication state
- Communicating with the backend API

---

## Server
The server is an Express application responsible for:
- Handling HTTP requests
- Authenticating users
- Enforcing authorization rules
- Applying business logic
- Interacting with the database

---

## Database
PostgreSQL is used to store application data, including:
- User accounts
- User-specific tasks

Each task belongs to exactly one user to ensure data isolation.

---

## Security Considerations
- Passwords are hashed before being stored
- JWTs are required to access protected routes
- Users can only access their own data
