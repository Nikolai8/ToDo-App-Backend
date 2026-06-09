# ToDo-App-Backend 📝

A full-stack task management application with a **Spring Boot REST API backend** and **React frontend**, built as a comprehensive study project demonstrating modern web application architecture.

## 📋 Project Overview

**ToDo-App** is a complete web application that allows users to create, read, update, and delete (CRUD) todo items with customizable priorities. The project demonstrates best practices in building scalable REST APIs, database design, and frontend integration.

The application was designed to showcase:
- Backend API design with Spring Boot and Spring Data JPA
- Database management with MySQL
- RESTful API principles and CORS handling
- Frontend integration with React
- Swagger/OpenAPI documentation

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
- 🔄 **CORS Support**: Cross-Origin Resource Sharing enabled
- 📱 **RESTful Design**: Standard HTTP methods (GET, POST, PUT, DELETE)
- 🗄️ **Database Management**: Automated Docker-based MySQL setup

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
- JavaScript: 42.7%
- Java: 22.6%
- CSS: 20.5%
- HTML: 14.2%

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

## 📡 API Endpoints

### Base URL: `http://localhost:8080/todos`

#### GET Requests
```bash
# Get all todo items
GET /todos/

# Get todo item by name/ID
GET /todos/{name}
```

#### POST Requests
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

#### PUT Requests
```bash
# Update todo item
PUT /todos/
Body:
{
  "todo": "item name",
  "priority": 3
}
```

#### DELETE Requests
```bash
# Delete todo item by name/ID
DELETE /todos/{name}
```

## 🗄️ Database Schema

### TodoItem Table
```sql
CREATE TABLE todo_item (
  todo VARCHAR(255) PRIMARY KEY,
  priority INT DEFAULT 2
);
```

### TodoItem Entity
- **todo** (String): Task description (Primary Key)
- **priority** (int): Priority level (default: 2, range: 1-5)

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
├── Backend/                              # Spring Boot Backend
│   ├── src/
│   │   ├── main/java/com/app/todo/
│   │   │   ├── ApiController.java       # REST Controller (CRUD endpoints)
│   │   │   ├── TodoItem.java             # Entity class
│   │   │   ├── TodoRepositiory.java      # JPA Repository interface
│   │   │   └── TodoAppApplication.java   # Spring Boot main class
│   │   └── resources/
│   │       └── application.properties    # Configuration
│   ├── pom.xml                           # Maven dependencies
│   └── docker-compose.yml                # Docker compose for MySQL
│
├── Frontend/                             # React Frontend
│   ├── public/
│   ├── src/
│   │   ├── App.js
│   │   ├── App.css
│   │   └── index.js
│   ├── package.json
│   └── README.md
│
└── README.md                             # This file
```

## 🔗 Related Repositories

- **Frontend Repository**: [ToDo-App-Frontend](https://github.com/Nikolai8/ToDo-App-Frontend)
  - Complete React frontend for this backend API
  - User interface for managing todo items

## 🎓 Context

This project was developed as a comprehensive study project showcasing:

- **Backend Development**: RESTful API design with Spring Boot
- **Database Management**: MySQL integration and JPA/Hibernate
- **API Documentation**: Swagger/OpenAPI best practices
- **Frontend Integration**: React consuming REST APIs
- **Docker & Containerization**: Containerized database setup
- **CORS & Security**: Cross-origin handling and basic authentication
- **Full-Stack Architecture**: Complete end-to-end application development

## 🔧 Technical Details

### Spring Boot Configuration
- **Spring Data JPA**: For database operations
- **Spring Boot Actuator**: Application monitoring
- **DevTools**: Hot reload during development
- **Springdoc OpenAPI**: Automatic API documentation

### MySQL Connection
- **Driver**: MySQL Connector/J
- **Connection String**: `jdbc:mysql://localhost:3307/todo`
- **ORM**: JPA with Hibernate

### API Response Format
```json
{
  "todo": "Example Task",
  "priority": 2
}
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

*Developed as a comprehensive study project in web application architecture*
