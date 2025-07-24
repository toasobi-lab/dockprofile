# 🚀 User Profile CRUD Application

A modern, full-stack user profile management application built with Docker Compose. Features a beautiful React frontend with Tailwind CSS, a robust FastAPI backend with comprehensive logging, PostgreSQL database with persistent storage, and pgAdmin for database administration.

## ✨ Features

- **🎨 Beautiful UI**: Modern React interface with Tailwind CSS
- **⚡ Fast API**: FastAPI backend with automatic API documentation
- **🗄️ Persistent Database**: PostgreSQL with automatic table creation
- **🔧 Admin Panel**: pgAdmin for easy database management
- **📊 Comprehensive Logging**: Detailed backend logging for debugging
- **🐳 Docker Ready**: Complete containerized setup with Docker Compose

## 🚀 Tech Stack

- **Frontend**: React 18 + Tailwind CSS 3.4 (Port 3000)
- **Backend**: FastAPI 0.109 + SQLAlchemy 2.0 (Port 8000)
- **Database**: PostgreSQL 16 (Port 5432)
- **Database UI**: pgAdmin 4 (Port 5050)

**Version Details**
- **Python**: 3.12
- **Node.js**: 20
- **React**: 18.2.0
- **FastAPI**: 0.109.0
- **PostgreSQL**: 16
- **Tailwind CSS**: 3.4.1

**Architecture**:
```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Frontend  │    │   Backend   │    │ PostgreSQL  │    │   pgAdmin   │
│   React     │◄──►│   FastAPI   │◄──►│   Database  │◄──►│   Admin UI  │
│   Port 3000 │    │   Port 8000 │    │   Port 5432 │    │   Port 5050 │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
```

## 🚀 Quick Start

**Prerequisites**: Docker (v20.10+) and Docker Compose (v2.0+)

**Installation**:

1. **Clone the repository**
   ```bash
   git clone https://github.com/toasobi-lab/dockprofile.git
   cd dockprofile
   ```

2. **Start all services**
   ```bash
   docker compose up --build
   ```

3. **Access the applications**
   | Service | URL | Credentials |
   |---------|-----|-------------|
   | **Frontend** | http://localhost:3000 | - |
   | **Backend API** | http://localhost:8000 | - |
   | **API Documentation** | http://localhost:8000/docs | - |
   | **pgAdmin** | http://localhost:5050 | Email: `admin@admin.com`<br>Password: `admin` |
   | **PostgreSQL** | localhost:5432 | User: `postgres`<br>Password: `password`<br>Database: `userprofiles` |

**First Steps**:
1. Wait 2-3 minutes for services to start
2. Open http://localhost:3000
3. Create your first user profile
4. View database at http://localhost:5050



## 🔧 API Reference

| Method | Endpoint | Description | Request Body | Response |
|--------|----------|-------------|--------------|----------|
| `GET` | `/health` | Health check | - | `{"status": "healthy"}` |
| `GET` | `/users` | Get all users | - | `User[]` |
| `GET` | `/users/{id}` | Get user by ID | - | `User` |
| `POST` | `/users` | Create new user | `{"name": "string", "email": "string", "bio": "string?"}` | `User` |
| `PUT` | `/users/{id}` | Update user | `{"name": "string?", "email": "string?", "bio": "string?"}` | `User` |
| `DELETE` | `/users/{id}` | Delete user | - | `{"message": "User deleted successfully"}` |

**Examples**:

**Create User:**
```bash
curl -X POST "http://localhost:8000/users" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "bio": "Software Developer"
  }'
```

**Get All Users:**
```bash
curl -X GET "http://localhost:8000/users"
```

**Update User:**
```bash
curl -X PUT "http://localhost:8000/users/1" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Smith",
    "bio": "Senior Software Developer"
  }'
```

## 📊 Database

**Schema**:
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    bio TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Sample Data**:
```sql
INSERT INTO users (name, email, bio) VALUES 
('John Doe', 'john@example.com', 'Software Developer'),
('Jane Smith', 'jane@example.com', 'Product Manager'),
('Bob Wilson', 'bob@example.com', 'Data Scientist');
```

**Access**:
- **Host**: `localhost` (or `postgres` from containers)
- **Port**: `5432`
- **Database**: `userprofiles`
- **Username**: `postgres`
- **Password**: `password`

## 🐳 Docker

| Service | Image | Port | Features |
|---------|-------|------|----------|
| **Frontend** | Custom React | 3000 | Hot reload, Tailwind CSS, Axios |
| **Backend** | Custom FastAPI | 8000 | SQLAlchemy ORM, logging, CORS |
| **PostgreSQL** | postgres:16 | 5432 | Persistent volume, auto-init |
| **pgAdmin** | dpage/pgadmin4 | 5050 | Auto-configured connection |

**Details**:

#### Frontend Service
- **Base Image**: `node:20-alpine`
- **Framework**: React 18 with Tailwind CSS
- **Features**: Hot reload, responsive design, API integration
- **Health Check**: Built into React development server

#### Backend Service
- **Base Image**: `python:3.12-slim`
- **Framework**: FastAPI with Uvicorn
- **Features**: SQLAlchemy ORM, comprehensive logging, CORS
- **Health Check**: `GET /health` endpoint

#### PostgreSQL Service
- **Image**: `postgres:16`
- **Features**: Persistent storage, automatic database creation
- **Volumes**: `postgres_data:/var/lib/postgresql/data`

#### pgAdmin Service
- **Image**: `dpage/pgadmin4:latest`
- **Features**: Auto-configured PostgreSQL connection
- **Volumes**: `pgadmin_data:/var/lib/pgadmin`

## 📝 Logging

The backend includes comprehensive logging for debugging and monitoring:

**Types**:
- **🔍 Request Logging**: All incoming API calls with method, path, and response status
- **❌ Error Logging**: Detailed error messages with full stack traces
- **🗄️ Database Logging**: Connection success/failure and query execution
- **✅ Operation Logging**: CRUD operation success/failure with user details

**Format**:
```
2024-01-15 10:30:45 - main - INFO - Incoming request: POST /users
2024-01-15 10:30:45 - main - INFO - Created user with ID 1
2024-01-15 10:30:45 - main - INFO - Response status: 201
```

**Viewing**:
```bash
# View all logs
docker compose logs

# View specific service logs
docker compose logs backend
docker compose logs frontend
docker compose logs postgres

# Follow logs in real-time
docker compose logs -f backend
```

## 🛠️ Development

**Features**:

#### Backend Development
1. **Add new endpoints** in `backend/main.py`
2. **Create new models** in `backend/models.py`
3. **Define schemas** in `backend/schemas.py`
4. **Test with**: `docker compose up --build`

#### Frontend Development
1. **Add new components** in `frontend/src/components/`
2. **Update API calls** in `frontend/src/App.js`
3. **Style with Tailwind** CSS classes
4. **Test with**: Hot reload enabled automatically

**Database**:
1. **Update SQLAlchemy models** in `backend/models.py`
2. **Tables are auto-created** on backend startup
3. **For schema changes**: Restart the backend service

**Styling**:
- **Framework**: Tailwind CSS 3.4.1
- **Approach**: Mobile-first responsive design
- **Components**: Modular React components
- **Theme**: Customizable via `tailwind.config.js`

**Commands**:
```bash
# Start development environment
docker compose up --build

# Rebuild specific service
docker compose up --build backend

# View logs during development
docker compose logs -f

# Stop all services
docker compose down

# Clean up volumes (⚠️ removes data)
docker compose down -v
```



## 📁 Project Structure

```
dockprofile/
├── docker-compose.yml          # Main configuration
├── pgadmin-servers.json        # pgAdmin configuration
├── README.md                   # Documentation
├── .gitignore                  # Git ignore rules
├── backend/                    # FastAPI backend
│   ├── Dockerfile             # Backend container
│   ├── requirements.txt       # Python dependencies
│   ├── main.py               # API endpoints
│   ├── models.py             # Database models
│   ├── schemas.py            # Pydantic schemas
│   └── database.py           # Database utilities
└── frontend/                  # React frontend
    ├── Dockerfile            # Frontend container
    ├── package.json          # Node.js dependencies
    ├── tailwind.config.js    # Tailwind CSS config
    ├── postcss.config.js     # PostCSS config
    ├── public/               # Static files
    │   └── index.html       # Main HTML file
    └── src/                  # React source code
        ├── index.js         # React entry point
        ├── index.css        # Global styles
        ├── App.js           # Main component
        └── components/      # React components
            ├── Header.js    # Application header
            ├── UserForm.js  # User form
            ├── UserList.js  # User list
            └── UserCard.js  # User card
```

**Key Files**:

| File | Purpose |
|------|---------|
| `docker-compose.yml` | Orchestrates all 4 services (frontend, backend, postgres, pgadmin) |
| `pgadmin-servers.json` | Auto-configures pgAdmin to connect to PostgreSQL |
| `backend/main.py` | FastAPI application with CRUD endpoints and logging |
| `backend/models.py` | SQLAlchemy User model definition |
| `frontend/App.js` | Main React component with state management |
| `frontend/components/` | Reusable React components with Tailwind styling |

---

**Made with ❤️ using modern web technologies** 