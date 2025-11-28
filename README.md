# Task Management API

## Overview
This repository contains a backend RESTful API for managing employees and tasks for an internal company dashboard. The API is designed to be consumed by frontend applications and supports CRUD operations, relationships, filtering, and authentication (bonus).

## Tech Stack
- Node.js
- Express.js
- MongoDB (Mongoose)

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
| status     | String   | Task status (Open, In Progress, Done) |
| employee   | ObjectId | Linked employee ID         |

## Sample Data
- Demo data seeding script: `backend/scripts/seedDemoData.js`

## API Endpoints

### Employees
- `GET /employees` — List all employees
- `POST /employees` — Create a new employee
- `GET /employees/:id` — Get employee by ID

#### Example Request/Response
- **POST /employees**
  - Request:
    ```json
    {
      "name": "Jane Smith",
      "role": "Manager",
      "email": "jane@example.com"
    }
    ```
  - Response:
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
- `PUT /tasks/:id` — Update a task
- `DELETE /tasks/:id` — Delete a task

#### Example Request/Response
- **POST /tasks**
  - Request:
    ```json
    {
      "title": "Prepare report",
      "description": "Q4 financials",
      "status": "Open",
      "employee": "<employeeId>"
    }
    ```
  - Response:
    ```json
    {
      "id": "...",
      "title": "Prepare report",
      "description": "Q4 financials",
      "status": "Open",
      "employee": "<employeeId>"
    }
    ```

## Authentication (Bonus)
- Protected endpoints (create/update tasks) require JWT token in `Authorization` header.
- Public endpoints (view tasks) do not require authentication.

## Error Handling & Validation
- Input validation for all endpoints
- Consistent error responses and HTTP status codes
- Centralized error middleware: `backend/middleware/errorMiddleware.js`

## Logging
- Basic request logging implemented

## Testing
- Test endpoints using Postman or similar tools
- Example Postman collection included (if provided)

## Setup Instructions
1. Clone the repository
   ```powershell
   git clone <your-repo-url>
   cd <repo-folder>
   ```
2. Install dependencies
   ```powershell
   cd backend
   npm install
   ```
3. Configure environment variables
   - Create a `.env` file in the `backend` folder:
     ```env
     MONGO_URI=<your-mongodb-uri>
     JWT_SECRET=<your-jwt-secret>
     ```
4. Run the server
   ```powershell
   npm start
   ```

## Assumptions
- Each task is linked to one employee
- Employee emails are unique
- Only authenticated users can create/update tasks; anyone can view tasks

## License
MIT
