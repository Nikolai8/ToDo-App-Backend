# ToDo-App-Backend 📝

A full-stack task management application with a **Spring Boot REST API backend** and **React frontend**, built as a comprehensive study project demonstrating modern web application architecture, CRUD operations, microservices separation, and database management.

## 📋 Project Overview

**ToDo-App** is a complete web application that allows users to create, read, update, and delete (CRUD) todo items with customizable priorities. The project demonstrates best practices in building **scalable, separated backend and frontend architectures** with clear API contracts and microservices principles.

The application was designed to showcase:
- **CRUD Operations**: Complete data lifecycle management (Create, Read, Update, Delete)
- **Backend API Design**: Spring Boot REST API with proper separation of concerns
- **Database Management**: MySQL with Spring Data JPA for data persistence
- **Microservices Architecture**: Clear separation between Backend API service and Frontend application
- **RESTful API Principles**: Standard HTTP methods and status codes
- **Frontend-Backend Separation**: Independent React frontend consuming REST APIs
- **Swagger/OpenAPI Documentation**: Interactive API documentation

## 🎯 Features

### Core Functionality
- ✅ **Create Todo Items**: Add new tasks with default priority level
- ✅ **Read Todo Items**: Retrieve all tasks or search by name
- ✅ **Update Todo Items**: Modify task priorities and descriptions
- ✅ **Delete Todo Items**: Remove completed or unwanted tasks
- ✅ **Priority System**: Assign priority levels (1-5) to tasks
- ✅ **Persistent Storage**: All data saved in MySQL database

### Technical Features
- 🔐 **Authentication**: Basic authentication with default credentials
- 📊 **Swagger UI**: Interactive API documentation and testing
- 🔄 **CORS Support**: Cross-Origin Resource Sharing enabled for frontend communication
- 📱 **RESTful Design**: Standard HTTP methods (GET, POST, PUT, DELETE)
- 🗄️ **Database Management**: Automated Docker-based MySQL setup
- 🏗️ **Microservices Ready**: Backend and frontend run as separate, independent services

## 🛠️ Technology Stack

### Backend
- **Framework**: Spring Boot 2.7.5
- **Language**: Java 17
- **Database**: MySQL 8.0.31
- **ORM**: Spring Data JPA
- **API Documentation**: Springdoc OpenAPI (Swagger UI)
- **Build Tool**: Maven
- **Containerization**: Docker & Docker Compose

### Frontend
- **Framework**: React 18.2.0
- **Language**: JavaScript (ES6+)
- **Styling**: CSS
- **Build Tool**: Create React App

### Languages in Repository
- JavaScript (42.7%)
- Java (22.6%)
- CSS (20.5%)
- HTML (14.2%)

## 📱 Requirements

### Backend
- Docker & Docker Desktop (for MySQL)
- Maven 3.6+
- Java 17 or higher
- Git

### Frontend
- Node.js 14+
- npm 6+

## 🚀 Getting Started

### Backend Setup

#### 1. Start MySQL Database
```bash
# Navigate to backend folder
cd Backend

# Start Docker container with MySQL
docker compose up

# Alternative: Manual Docker command
docker run --name todoDB \
  -e MYSQL_ROOT_PASSWORD=your_password \
  -d \
  -e MYSQL_DATABASE=todo \
  -p 3307:3306 \
  mysql:8.0.31
```

**Database Details:**
- Container Name: `todoDB`
- Port: `3307` (mapped to container's 3306)
- Database: `todo`
- Root User: `root`

#### 2. Start Spring Boot Server
```bash
# Ensure you're in the Backend folder
cd Backend

# Open project in Maven/IDE or use command line
mvn spring-boot:run

# Server will start on http://localhost:8080
```

#### 3. Access the Application
- **Application Root**: [http://localhost:8080/](http://localhost:8080/)
- **Swagger UI**: [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)
- **API Documentation**: [http://localhost:8080/v3/api-docs/](http://localhost:8080/v3/api-docs/)

**Default Credentials:**
- Password: `123456`

### Frontend Setup

#### 1. Install Dependencies
```bash
cd Frontend
npm install
```

#### 2. Start Development Server
```bash
npm start
```

The frontend will open automatically at [http://localhost:3000](http://localhost:3000)

#### 3. Build for Production
```bash
npm run build
```

## 📚 CRUD Operations Explained

CRUD stands for **Create, Read, Update, Delete** - the four fundamental operations for data management:

### Create (POST)
- **Purpose**: Add new data to the system
- **HTTP Method**: POST
- **Endpoint**: `POST /todos/?name=task_name`
- **What happens**: A new todo item is created in the database with default priority (2)
- **Example**:
  ```bash
  curl -X POST "http://localhost:8080/todos/?name=Buy%20groceries"
  ```
- **Response**: New TodoItem object with the task name and priority

### Read (GET)
- **Purpose**: Retrieve existing data from the system
- **HTTP Method**: GET
- **Endpoints**:
  - `GET /todos/` - Get all todo items
  - `GET /todos/{name}` - Get specific todo item by name
- **What happens**: Data is fetched from the database without modification
- **Example**:
  ```bash
  curl -X GET "http://localhost:8080/todos/"
  ```
- **Response**: List of all TodoItem objects or specific item

### Update (PUT)
- **Purpose**: Modify existing data
- **HTTP Method**: PUT
- **Endpoint**: `PUT /todos/`
- **Body**:
  ```json
  {
    "todo": "item name",
    "priority": 3
  }
  ```
- **What happens**: Finds the todo item by name and updates its priority
- **Example**:
  ```bash
  curl -X PUT "http://localhost:8080/todos/" \
    -H "Content-Type: application/json" \
    -d '{"todo":"Buy groceries","priority":4}'
  ```
- **Response**: Updated TodoItem object

### Delete (DELETE)
- **Purpose**: Remove data from the system
- **HTTP Method**: DELETE
- **Endpoint**: `DELETE /todos/{name}`
- **What happens**: Finds and removes the todo item from the database
- **Example**:
  ```bash
  curl -X DELETE "http://localhost:8080/todos/Buy%20groceries"
  ```
- **Response**: Success status

## 🗄️ Database Architecture

### Database Purpose
The MySQL database is the **persistent storage layer** for all todo items. It ensures data survives application restarts and allows multiple clients to access the same data.

### Database Schema

```sql
CREATE TABLE todo_item (
  todo VARCHAR(255) PRIMARY KEY,
  priority INT DEFAULT 2
);
```

### TodoItem Table Structure
| Column | Type | Description |
|--------|------|-------------|
| **todo** | VARCHAR(255) | Task description (Primary Key - unique identifier) |
| **priority** | INT | Priority level (default: 2, range: 1-5) |

### Data Flow
1. **Frontend** → sends HTTP request to Backend API
2. **Backend API** → processes request and calls Repository
3. **Repository** → uses JPA to interact with Database
4. **Database** → stores/retrieves data (persistent)
5. **Backend API** → returns JSON response to Frontend
6. **Frontend** → displays data to user

### MySQL Connection Details
- **Connection String**: `jdbc:mysql://localhost:3307/todo`
- **ORM**: JPA with Hibernate (automatic SQL generation)
- **Driver**: MySQL Connector/J

## 📡 API Endpoints & REST Principles

### Base URL: `http://localhost:8080/todos`

The API follows **RESTful principles**, using standard HTTP methods to represent actions on resources:

#### GET Requests (Read)
```bash
# Get all todo items
GET /todos/

# Get todo item by name/ID
GET /todos/{name}
```

#### POST Requests (Create)
```bash
# Create new todo item
POST /todos/
Query Parameters:
  - name: string (required)
```

Example:
```bash
curl -X POST "http://localhost:8080/todos/?name=Buy%20groceries"
```

#### PUT Requests (Update)
```bash
# Update todo item
PUT /todos/
Body:
{
  "todo": "item name",
  "priority": 3
}
```

#### DELETE Requests (Delete)
```bash
# Delete todo item by name/ID
DELETE /todos/{name}
```

### API Response Format
```json
{
  "todo": "Example Task",
  "priority": 2
}
```

### HTTP Status Codes
- **200 OK**: Request successful
- **201 Created**: Resource created successfully
- **400 Bad Request**: Invalid input
- **404 Not Found**: Resource not found
- **500 Internal Server Error**: Server error

## 🏗️ Microservices Architecture

This project demonstrates **microservices separation of concerns** by splitting the application into independent services:

### Architecture Overview
```
┌─────────────────────────────────────────────────────────┐
│                    CLIENT BROWSER                        │
└────────────────┬────────────────────────────────────────┘
                 │
                 │ HTTP/REST
                 │
    ┌────────────▼──────────────┐
    │   Frontend Service        │
    │   (React - Port 3000)     │
    │   - UI Components         │
    │   - User Interaction      │
    │   - API Calls             │
    └────────────┬──────────────┘
                 │
                 │ HTTP/REST
                 │ CORS Enabled
                 │
    ┌────────────▼──────────────┐
    │   Backend Service         │
    │  (Spring Boot - 8080)     │
    │   - REST API Endpoints    │
    │   - Business Logic        │
    │   - Data Processing       │
    └────────────┬──────────────┘
                 │
                 │ JDBC/SQL
                 │
    ┌────────────▼──────────────┐
    │   Database Service        │
    │  (MySQL - Port 3307)      │
    │   - Data Storage          │
    │   - Data Persistence      │
    │   - Query Processing      │
    └──────────────────────────┘
```

### Service Separation

#### Frontend Service (React)
- **Port**: 3000
- **Responsibility**: User interface and client-side logic
- **Technology**: React 18.2.0 + JavaScript
- **Communication**: HTTP REST calls to Backend API
- **Features**:
  - Displays todo list
  - Form inputs for creating/editing tasks
  - Calls Backend API for all data operations
  - Handles user interactions

#### Backend Service (Spring Boot)
- **Port**: 8080
- **Responsibility**: Business logic, data processing, API endpoints
- **Technology**: Spring Boot 2.7.5 + Java 17
- **Communication**:
  - Receives HTTP requests from Frontend
  - Queries Database via JPA
  - Returns JSON responses
- **Features**:
  - CRUD operations
  - Data validation
  - Authentication
  - CORS handling
  - Swagger documentation

#### Database Service (MySQL)
- **Port**: 3307 (mapped from 3306)
- **Responsibility**: Persistent data storage
- **Technology**: MySQL 8.0.31 in Docker
- **Communication**: JDBC/SQL with Backend
- **Features**:
  - Data persistence
  - ACID compliance
  - Indexed queries
  - Data integrity

### Why Microservices Architecture?

1. **Independence**: Each service can be deployed separately
2. **Scalability**: Services can be scaled individually
3. **Maintainability**: Clear separation of concerns
4. **Technology Flexibility**: Each service can use different technologies
5. **Development Efficiency**: Teams can work on services independently
6. **Reusability**: Backend API can serve multiple frontend clients
7. **Fault Isolation**: One service failure doesn't crash others

### Inter-Service Communication

#### Frontend ↔ Backend Communication
- **Protocol**: HTTP REST
- **Port**: 8080
- **Format**: JSON
- **CORS**: Enabled to allow cross-origin requests
- **Example**:
  ```javascript
  // React Frontend calling Backend API
  fetch('http://localhost:8080/todos/')
    .then(response => response.json())
    .then(data => console.log(data))
  ```

#### Backend ↔ Database Communication
- **Protocol**: JDBC/SQL
- **Port**: 3307
- **Format**: SQL queries via JPA
- **Example**:
  ```java
  // Spring Boot Backend querying Database
  List<TodoItem> todos = repository.findAll();
  ```

## 📊 Swagger UI Usage

The **Swagger UI** provides an interactive interface to test all API endpoints:

1. Navigate to [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)
2. Expand each endpoint to see details
3. Click "Try it out" to test endpoints
4. Enter parameters and execute requests
5. View responses in real-time

## 📂 Project Structure

```
ToDo-App/
├── Backend/                              # Spring Boot Backend Service
│   ├── src/
│   │   ├── main/java/com/app/todo/
│   │   │   ├── ApiController.java       # REST Controller (API Endpoints)
│   │   │   ├── TodoItem.java             # Entity class (Database model)
│   │   │   ├── TodoRepository.java       # JPA Repository (Database access)
│   │   │   └── TodoAppApplication.java   # Spring Boot main class
│   │   └── resources/
│   │       └── application.properties    # Backend configuration
│   ├── pom.xml                           # Maven dependencies
│   └── docker-compose.yml                # Docker compose for MySQL
│
├── Frontend/                             # React Frontend Service
│   ├── public/
│   ├── src/
│   │   ├── App.js                        # Main React component
│   │   ├── App.css                       # Styling
│   │   └── index.js                      # Entry point
│   ├── package.json                      # Frontend dependencies
│   └── README.md                         # Frontend docs
│
└── README.md                             # This file
```

## 🔗 Related Repositories

- **Frontend Repository**: [ToDo-App-Frontend](https://github.com/Nikolai8/ToDo-App-Frontend)
  - Complete React frontend for this backend API
  - User interface for managing todo items

## 🎓 Learning Outcomes

This project was developed as a comprehensive study project showcasing:

- **CRUD Operations**: Complete understanding of Create, Read, Update, Delete cycles
- **REST API Design**: Proper HTTP method usage and RESTful principles
- **Backend Development**: Spring Boot framework and application structure
- **Database Management**: MySQL integration, schema design, and data persistence
- **Microservices Architecture**: Service separation and independent deployment
- **API Documentation**: Swagger/OpenAPI best practices
- **Frontend-Backend Integration**: React consuming REST APIs
- **Docker & Containerization**: Containerized database setup
- **CORS & Security**: Cross-origin handling and authentication
- **Full-Stack Architecture**: Complete end-to-end application development
- **Inter-Service Communication**: How different services communicate over HTTP and JDBC

## 🔧 Technical Details

### Spring Boot Configuration
- **Spring Data JPA**: For database operations with automatic SQL generation
- **Spring Boot Actuator**: Application monitoring and health checks
- **DevTools**: Hot reload during development
- **Springdoc OpenAPI**: Automatic Swagger documentation generation

### MySQL Connection
- **Driver**: MySQL Connector/J
- **Connection String**: `jdbc:mysql://localhost:3307/todo`
- **ORM**: JPA with Hibernate for object-relational mapping

### CORS Configuration
Enables frontend (port 3000) to communicate with backend (port 8080):
```
Access-Control-Allow-Origin: http://localhost:3000
```

## 🐛 Troubleshooting

### Docker Issues
```bash
# Stop and remove existing container
docker stop todoDB
docker rm todoDB

# Restart fresh container
docker compose up
```

### Maven/Spring Boot Issues
```bash
# Clean and rebuild
mvn clean install
mvn spring-boot:run
```

### Port Already in Use
- Backend (8080): Change in `application.properties`
- Frontend (3000): npm will prompt to use different port
- MySQL (3307): Change port mapping in docker-compose.yml

### Database Connection Issues
- Ensure Docker container is running: `docker ps`
- Check credentials in `application.properties`
- Verify database name and port
- Verify CORS is enabled for frontend communication

### Frontend Cannot Connect to Backend
- Ensure Backend is running on port 8080
- Check CORS is properly configured
- Verify Frontend is trying to connect to `http://localhost:8080`
- Check browser console for network errors

## 📝 License

This project is licensed under the **MIT License with Educational Use Only Clause**.

**Important**:
- ✅ Use, modification, and learning for **educational purposes allowed**
- ❌ **Commercial use prohibited** (without explicit permission)
- ❌ **Copy-paste as your own project/homework prohibited**
- ✅ **Attribution required** when using

See [LICENSE](LICENSE) for full details.

## 🤝 Contributing

Questions or suggestions for improvements? Feel free to create issues or start discussions!

---

**Built with ❤️ as a full-stack learning project**

*Developed as a comprehensive study project in web application architecture, microservices, CRUD operations, and database management*
