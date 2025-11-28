# Task Management API

## Overview
This project is a backend RESTful API for managing employees and tasks in an internal company dashboard. It allows frontend applications to perform CRUD operations on employees and tasks, link tasks to employees, and filter tasks by status or employee.

## Tech Stack
- Node.js
- Express.js
- MongoDB (via Mongoose)

## Features
- Create and list employees
- Create, update, retrieve, and delete tasks
- Link tasks to employees
- Filter tasks by status or employee
- Modular code structure (routes, models, controllers, services)
- Error handling and validation
- Basic logging
- Proper HTTP status codes
- (Bonus) JWT authentication for protected endpoints

## Setup Instructions

1. **Clone the repository**
   ```powershell
   git clone <your-repo-url>
   cd <repo-folder>
   ```
2. **Install dependencies**
   ```powershell
   cd backend
   npm install
   ```
3. **Configure environment variables**
   - Create a `.env` file in the `backend` folder with the following:
     ```env
     MONGO_URI=<your-mongodb-uri>
     JWT_SECRET=<your-jwt-secret>
     ```
4. **Run the server**
   ```powershell
   npm start
   ```

## Database Schema

### Employee
| Field | Type    | Description         |
|-------|---------|---------------------|
| id    | ObjectId| Unique employee ID  |
| name  | String  | Employee name       |
| role  | String  | Job role            |
| email | String  | Contact email       |

### Task
| Field      | Type     | Description                |
|------------|----------|----------------------------|
| id         | ObjectId | Unique task ID             |
| title      | String   | Task title                 |
| description| String   | Task details               |
| status     | String   | Task status (e.g., Open, In Progress, Done) |
| employee   | ObjectId | Linked employee ID         |

## Sample Data
- See `backend/scripts/seedDemoData.js` for demo data seeding.

## API Endpoints

### Employees
- `GET /employees` — List all employees
  - **Response:**
    ```json
    [
      {
        "id": "...",
        "name": "John Doe",
        "role": "Developer",
        "email": "john@example.com"
      }
    ]
    ```
- `POST /employees` — Create a new employee
  - **Request:**
    ```json
    {
      "name": "Jane Smith",
      "role": "Manager",
      "email": "jane@example.com"
    }
    ```
  - **Response:**
    ```json
    {
      "id": "...",
      "name": "Jane Smith",
      "role": "Manager",
      "email": "jane@example.com"
    }
    ```

### Tasks
- `GET /tasks` — List all tasks
- `GET /tasks?status=In%20Progress` — Filter tasks by status
- `GET /tasks?employee=<employeeId>` — Filter tasks by employee
- `POST /tasks` — Create a new task
  - **Request:**
    ```json
    {
      "title": "Prepare report",
      "description": "Q4 financials",
      "status": "Open",
      "employee": "<employeeId>"
    }
    ```
- `PUT /tasks/:id` — Update a task
- `DELETE /tasks/:id` — Delete a task

## Authentication (Bonus)
- Protected endpoints (create/update tasks) require JWT token in `Authorization` header.
- Public endpoints (view tasks) do not require authentication.

## Error Handling & Validation
- All endpoints validate input and return appropriate error messages and HTTP status codes.
- Errors are handled via middleware (`backend/middleware/errorMiddleware.js`).

## Logging
- Basic request logging is implemented.

## Testing
- Use Postman or similar tools to test endpoints.
- Example Postman collection included (if provided).

## Assumptions
- Each task is linked to one employee.
- Email addresses are unique for employees.
- Only authenticated users can create/update tasks; anyone can view tasks.

## Folder Structure
```
backend/
  config/
  controllers/
  middleware/
  models/
  routes/
  scripts/
  services/
  utils/
  server.js
  package.json
```

## License
MIT
