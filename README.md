# Task CRUD Application

A complete Express.js CRUD application with MongoDB and Mongoose for managing tasks.

## Features

- ✅ Create a new task
- ✅ Get all tasks
- ✅ Get a single task by ID
- ✅ Update a task
- ✅ Delete a task

## Tech Stack

- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - MongoDB object modeling
- **dotenv** - Environment variable management

## Project Structure

```
crud_app/
├── config/
│   └── db.js              # MongoDB connection configuration
├── controllers/
│   └── taskController.js  # Task business logic
├── models/
│   └── Task.js            # Task Mongoose model
├── routes/
│   └── taskRoutes.js      # Task route definitions
├── .env.example           # Environment variables template
├── package.json           # Project dependencies
├── README.md             # Project documentation
└── server.js             # Application entry point
```

## Task Model

The Task model includes the following fields:

- **title** (String, required) - Task title
- **description** (String, optional) - Task description
- **completed** (Boolean, default: false) - Task completion status
- **createdAt** (Date, auto-generated) - Creation timestamp
- **updatedAt** (Date, auto-generated) - Last update timestamp

## Installation

1. **Clone or navigate to the project directory:**
   ```bash
   cd crud_app
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Set up environment variables:**
   ```bash
   cp .env.example .env
   ```
   
   Edit `.env` and update the MongoDB URI:
   ```
   MONGODB_URI=mongodb://localhost:27017/taskdb
   ```

4. **Make sure MongoDB is running:**
   - If using local MongoDB, ensure the MongoDB service is running
   - For MongoDB Atlas, update the `MONGODB_URI` in `.env` with your connection string

## Running the Application

**Start the server:**
```bash
npm start
```

Or for development with auto-reload:
```bash
npm run dev
```

The server will start on `http://localhost:3000` (or the port specified in `.env`).

## API Endpoints

### Base URL
```
http://localhost:3000/api/tasks
```

### Endpoints

#### 1. Get All Tasks
```http
GET /api/tasks
```

**Response:**
```json
{
  "success": true,
  "count": 2,
  "data": [
    {
      "_id": "65a1b2c3d4e5f6g7h8i9j0k1",
      "title": "Sample Task",
      "description": "This is a sample task",
      "completed": false,
      "createdAt": "2024-01-15T10:30:00.000Z",
      "updatedAt": "2024-01-15T10:30:00.000Z"
    }
  ]
}
```

#### 2. Create a Task
```http
POST /api/tasks
Content-Type: application/json

{
  "title": "New Task",
  "description": "Task description",
  "completed": false
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "_id": "65a1b2c3d4e5f6g7h8i9j0k1",
    "title": "New Task",
    "description": "Task description",
    "completed": false,
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T10:30:00.000Z"
  }
}
```

#### 3. Get Single Task
```http
GET /api/tasks/:id
```

**Response:**
```json
{
  "success": true,
  "data": {
    "_id": "65a1b2c3d4e5f6g7h8i9j0k1",
    "title": "Sample Task",
    "description": "Task description",
    "completed": false,
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T10:30:00.000Z"
  }
}
```

#### 4. Update a Task
```http
PUT /api/tasks/:id
Content-Type: application/json

{
  "title": "Updated Task",
  "description": "Updated description",
  "completed": true
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "_id": "65a1b2c3d4e5f6g7h8i9j0k1",
    "title": "Updated Task",
    "description": "Updated description",
    "completed": true,
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T11:00:00.000Z"
  }
}
```

#### 5. Delete a Task
```http
DELETE /api/tasks/:id
```

**Response:**
```json
{
  "success": true,
  "message": "Task deleted successfully",
  "data": {}
}
```

## Error Handling

The application includes comprehensive error handling:

- **404 Not Found** - When a task or route is not found
- **400 Bad Request** - When validation fails
- **500 Internal Server Error** - For server errors

Error response format:
```json
{
  "success": false,
  "message": "Error message here"
}
```

## Testing with cURL

### Create a task:
```bash
curl -X POST http://localhost:3000/api/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Test Task","description":"This is a test","completed":false}'
```

### Get all tasks:
```bash
curl http://localhost:3000/api/tasks
```

### Get a single task:
```bash
curl http://localhost:3000/api/tasks/TASK_ID
```

### Update a task:
```bash
curl -X PUT http://localhost:3000/api/tasks/TASK_ID \
  -H "Content-Type: application/json" \
  -d '{"title":"Updated Task","description":"Updated","completed":true}'
```

### Delete a task:
```bash
curl -X DELETE http://localhost:3000/api/tasks/TASK_ID
```

## License

ISC

