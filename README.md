# FastAPI Todo App

A simple backend API for managing personal todo items with user authentication, role-based admin access, and a MySQL database. The project demonstrates core FastAPI concepts such as routing, dependency injection, JWT authentication, SQLAlchemy ORM, and Pydantic validation.

## Features

- User registration and login
- JWT-based authentication with OAuth2 password flow
- Secure password hashing with `passlib`
- Todo CRUD operations tied to the authenticated user
- Admin-only access to all todos
- Database persistence with SQLAlchemy and MySQL
- Auto-generated API docs with Swagger UI and ReDoc
- Request validation using Pydantic models

## Tech Stack

- Python 3.14+
- FastAPI
- SQLAlchemy
- MySQL / PyMySQL
- JWT (`python-jose`)
- Passlib + bcrypt
- Uvicorn

## Project Structure

```text
FastApi-TodoApp/
├── main.py
├── database.py
├── models.py
├── requirements.txt
├── routers/
│   ├── __init__.py
│   ├── admin.py
│   ├── auth.py
│   ├── todos.py
│   └── users.py
└── README.md
```

## Prerequisites

Before running the app, make sure you have:

- Python installed
- MySQL server running locally
- A database named `TodoAppDB`
- A virtual environment (recommended)

## Setup

1. Clone the repository:

2. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Create the MySQL database:

```sql
CREATE DATABASE TodoAppDB;
```

5. Ensure the database connection in `database.py` matches your local setup:

```python
SQLALCHEMY_DATABASE_URL = "mysql+pymysql://root:root@127.0.0.1:3306/TodoAppDB"
```

> Note: This project currently stores the database credentials and JWT secret directly in code. For production use, move them to environment variables.

## Run the Application

Start the API server with:

```bash
uvicorn main:app --reload
```

The app will be available at:

- API: http://127.0.0.1:8000
- Swagger docs: http://127.0.0.1:8000/docs
- ReDoc: http://127.0.0.1:8000/redoc

## API Overview

### Authentication

- `POST /auth/` — Register a new user
- `POST /auth/token` — Login and receive a JWT token

### User

- `GET /user/` — Fetch the authenticated user's profile
- `PUT /user/password` — Change the authenticated user's password

### Todos

- `GET /` — List todos owned by the authenticated user
- `GET /todo/{todo_id}` — Get a specific todo by id
- `POST /todo` — Create a new todo
- `PUT /todo/{todo_id}` — Update a todo
- `DELETE /todo/{todo_id}` — Delete a todo

### Admin

- `GET /admin/todo` — View all todos (admin-only)
- `DELETE /admin/todo/{todo_id}` — Delete any todo (admin-only)
