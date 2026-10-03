# Student Management System

A REST API built with Spring Boot and JPA/Hibernate for managing students, courses, and enrollments.

## Features

- Full CRUD operations for Students, Courses, and Enrollments
- Many-to-many relationship between Students and Courses via a dedicated Enrollment entity (tracks enrollment date and grade)
- Input validation (required fields, minimum values)
- Custom exception handling with proper HTTP status codes (404 for not found, 400 for invalid input)
- MySQL database with Hibernate auto-schema generation

## Tech Stack

- Java 25
- Spring Boot 4.1.1
- Spring Data JPA / Hibernate
- MySQL
- Maven

## Entity Relationships

```
Student (1) ----< Enrollment >---- (1) Course
```

Each `Enrollment` links one student to one course, with its own `enrollmentDate` and `grade`.

## API Endpoints

### Students
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/students` | Get all students |
| GET | `/students/{id}` | Get a student by id |
| POST | `/students` | Create a student |
| DELETE | `/students/{id}` | Delete a student |

### Courses
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/courses` | Get all courses |
| GET | `/courses/{id}` | Get a course by id |
| POST | `/courses` | Create a course |
| DELETE | `/courses/{id}` | Delete a course |

### Enrollments
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/enrollments` | Get all enrollments |
| GET | `/enrollments/{id}` | Get an enrollment by id |
| POST | `/enrollments` | Create an enrollment (links a student + course) |
| DELETE | `/enrollments/{id}` | Delete an enrollment |

## Example Request

**POST /students**
```json
{
    "name": "Alice",
    "yearOfStudy": 2
}
```

**POST /enrollments**
```json
{
    "student": { "id": 1 },
    "course": { "id": 1 },
    "enrollmentDate": "2026-10-03",
    "grade": "A"
}
```

## Running Locally

1. Clone the repo
2. Create a MySQL database named `studentdb`
3. Add your own `src/main/resources/application.properties` with your database credentials (this file is gitignored):
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/studentdb
   spring.datasource.username=root
   spring.datasource.password=yourpassword
   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.show-sql=true
   ```
4. Run the application:
   ```
   ./mvnw spring-boot:run
   ```
5. The API will be available at `http://localhost:8080`