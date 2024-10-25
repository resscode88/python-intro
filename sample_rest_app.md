# FastAPI CRUD Microservice

This is a sample FastAPI-based microservice with CRUD operations for `users` and `user_roles`, where both are stored and retrieved from a PostgreSQL database. The project is organized following a modern approach, using FastAPI, SQLAlchemy, Alembic, and PostgreSQL.

## Project Structure

```bash
my_microservice/
│
├── app/
│   ├── api/
│   │   ├── __init__.py
│   │   ├── users.py         # API endpoints for users
│   │   └── user_roles.py    # API endpoints for user roles
│   ├── core/
│   │   ├── __init__.py
│   │   ├── config.py        # Database and environment configuration
│   ├── crud/
│   │   ├── __init__.py
│   │   ├── user.py          # CRUD operations for users
│   │   └── user_role.py     # CRUD operations for user roles
│   ├── db/
│   │   ├── __init__.py
│   │   ├── base.py          # Base class for SQLAlchemy models
│   │   └── session.py       # Database session management
│   ├── models/
│   │   ├── __init__.py
│   │   ├── user.py          # SQLAlchemy models for users
│   │   └── user_role.py     # SQLAlchemy models for user roles
│   ├── schemas/
│   │   ├── __init__.py
│   │   ├── user.py          # Pydantic schemas for users
│   │   └── user_role.py     # Pydantic schemas for user roles
│   └── main.py              # Application entry point
│
├── alembic/                 # Directory for database migrations
│
├── alembic.ini              # Alembic configuration file
├── requirements.txt         # Required libraries
└── .env                     # Environment variables (DB credentials)
```

## Setup Environment

### Create and Activate Virtual Environment

```bash
# Create a virtual environment
python -m venv venv

# Activate the virtual environment
# On Linux/MacOS:
source venv/bin/activate

# On Windows:
venv\Scripts\activate
```

### Install Dependencies
```bash
# Install all the dependencies listed in the requirements.txt file
pip install -r requirements.txt
```

### Environment Variables
Create a .env file in the root of your project to store environment variables like database connection strings.

```bash
# Example .env:
DATABASE_URL=postgresql://user:password@localhost/mydb
```

## Database Migrations (Alembic)
Alembic handles schema migrations for the PostgreSQL database.

3.1. Initialize Alembic
```bash
alembic init alembic
```

### Create and Apply Migrations
```bash
# Generate a migration script based on changes in the models
alembic revision --autogenerate -m "Initial migration"

# Apply the migration to the database
alembic upgrade head
```
 
## Running the Application
Run the FastAPI application using Uvicorn, which serves the app.

```bash
uvicorn app.main:app --reload
#The app will be available at http://127.0.0.1:8000.
#The --reload flag ensures that the server restarts when code changes are detected during development.
```

## Common Development Commands
Task	Command
Create virtual environment	python -m venv venv
Activate virtual environment	source venv/bin/activate (Linux/MacOS) or venv\Scripts\activate (Windows)
Install dependencies	pip install -r requirements.txt
Run the FastAPI app	uvicorn app.main:app --reload
Generate migration	alembic revision --autogenerate -m "message"
Apply migration	alembic upgrade head
Run tests (if any)	pytest
Deactivate virtual environment	deactivate
 
## Optional: Docker Support
You can containerize your application using Docker.

Example Dockerfile:

```Dockerfile

FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

Example docker-compose.yml:
```yaml
version: '3'

services:
  web:
    build: .
    ports:
      - "8000:8000"
    env_file:
      - .env
    depends_on:
      - db
  db:
    image: postgres
    restart: always
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

## Running with Docker
To build and run the app using Docker:

```bash
docker-compose up --build
```

## Additional Commands
Install New Packages:

*To install a new package, use:*

```bash
pip install <package-name>
pip freeze > requirements.txt  # Update the requirements file
```

### Virtual Environment:

*To deactivate the virtual environment:*

```bash
deactivate
```
