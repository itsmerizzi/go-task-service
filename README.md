# go-task-service
This project is a task management microservice built in Golang, created as part of a study project to explore Golang's capabilities for building API-based applications. It includes endpoints for creating and listing tasks, and utilizes channels and goroutines to manage task processing concurrently.

### Features
 - Create and List Tasks: Supports creating new tasks with a "pending" status and retrieving all tasks.
 - Concurrent Task Processing: Uses channels and goroutines to handle task processing, making it efficient and ideal for concurrent task management.
 - SQLite Database: Persists task data in a SQLite database, allowing the service to store task information between service restarts.

### Requirements
 - Go 1.16+
 - SQLite3

### Getting Started...

#### Installation
 1. Clone the repository:
```
git clone https://github.com/yourusername/task-service.git
cd task-service
```

 2. Install dependencies: This service uses the SQLite driver, which you can install with:
```
go get -u github.com/mattn/go-sqlite3
```

3. Set up SQLite database: Make sure to have `tasks.db` in the same directory. You can create this file manually or let the service generate it on the first run if the database is empty.

### Running the Service
 - Run the server:
```
go run main.go
```
 - The server will start on http://localhost:8081. Use a tool like curl or Postman to interact with the API.

### API Endpoints

#### Create a Task
 - Endpoint: POST /tasks
 - Description: Creates a new task with a "pending" status and adds it to the task queue for processing.
 - Request Body:
```json
{
  "title": "Task Title",
  "description": "Detailed description of the task"
}
```
 - Response:
   - 201 Created if successful
   - 400 Bad Request if there is an error with the request format

#### List All Tasks
 - Endpoint: GET /tasks
 - Description: Returns a list of all tasks with their status.
 - Response:
```json
[
  {
    "id": 1,
    "title": "Sample Task",
    "description": "Task description",
    "status": "completed",
    "created_at": "2023-08-01T14:48:00Z"
  },
  ...
]
```

### Code Overview
#### Key Components
 - Task Struct: Defines a task with attributes like ID, Title, Description, Status, and CreatedAt.
 - TaskService Struct: Encapsulates task-related functions, including:
   - AddTask: Inserts a new task into the database.
   - UpdateTaskStatus: Updates the status of a task.
   - ListTasks: Retrieves all tasks from the database.
   - ProcessTasks: Processes tasks in the queue asynchronously.

#### Concurrency
The service uses a Goroutine for ProcessTasks, continuously monitoring a channel for new tasks and processing them. This allows each task to be processed without blocking other requests, demonstrating the efficiency of Golang's concurrency model.

#### Future Improvements
 - Implement authentication and authorization for API endpoints.
 - Add more fields to Task, such as priority or due dates.
 - Create additional endpoints for updating and deleting tasks.
 - Integrate with a more robust database like PostgreSQL or MySQL.

#### Contributions
Feel free to open an issue or submit a pull request for any improvements or bug fixes!
