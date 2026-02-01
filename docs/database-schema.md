# Tasktt – Database Schema

## Overview
Tasktt uses a PostgreSQL relational database to store user accounts and
user-specific tasks.

The schema is designed to:
- Enforce data ownership
- Prevent users from accessing other users’ data
- Support authentication and task management features

---

## Tables

### users
Stores registered user accounts.

| Column         | Type        | Constraints                    |
|---------------|------------|--------------------------------|
| id            | UUID        | Primary key                    |
| email         | VARCHAR     | Unique, not null               |
| password_hash | TEXT        | Not null                       |
| created_at    | TIMESTAMP   | Default CURRENT_TIMESTAMP      |

---

### tasks
Stores tasks created by users.

| Column       | Type        | Constraints                                  |
|-------------|------------|----------------------------------------------|
| id          | SERIAL     | Primary key                                  |
| user_id    | UUID       | Foreign key → users(id), not null            |
| title       | VARCHAR    | Not null                                     |
| description | TEXT       | Optional                                     |
| completed  | BOOLEAN    | Default false                                |
| due_date   | DATE       | Optional                                     |
| created_at | TIMESTAMP  | Default CURRENT_TIMESTAMP                    |

---

## Relationships

- A **user** can have many tasks
- A **task** belongs to exactly one user

This relationship is enforced using a foreign key constraint
on `tasks.user_id`.

---

## Data Ownership & Security

All task queries must include the authenticated user’s ID.
This ensures that:
- Users can only view their own tasks
- Users cannot modify or delete tasks they do not own

Example authorization condition:

```sql
WHERE tasks.user_id = authenticated_user_id
