# Application Overview
Easygenerator Auth app task

## Main Repository

- **Repository Name**: authapp
- **Description**: The main repository for the Auth App project, which includes submodules for frontend and backend services.

## Components

The application consists of four main components:

1. **Frontend**
   - **Description**: A React-based frontend application that serves the user interface. It is designed to communicate with the backend service to Sign-up and Sign-in the user.
   - **Port**: Exposed on port 3000.
   - **Environment Variable**:
     - `REACT_APP_API_BASE_URL`: Points to the backend service URL.

2. **Backend**
   - **Description**: A NestJS-based backend application that handles business logic, user authentication, and data management. It connects to both MongoDB and Redis for persistent storage and caching.
   - **Port**: Exposed on port 3001.
   - **Environment Variables**:
     - `MONGO_URI`: Connection string for MongoDB.
     - `JWT_SECRET`: Secret key for JWT authentication.
     - `REDIS_HOST`: Host address for Redis.
     - `REDIS_PORT`: Port number for Redis.

3. **MongoDB**
   - **Description**: A NoSQL database used for storing application data.
   - **Port**: Exposed on port 27017.
   - **Initial Setup**: Includes root credentials and an initial database setup.

4. **Redis**
   - **Description**: An in-memory data structure store used for caching and session management.
   - **Port**: Exposed on port 6379.

## Workflow


- **Authentication** frontend send the login or signup credentials to backend and backend after validating or creating a new user sets the access_token as http-only cookie for frontend.
- **Frontend** communicates with the **Backend** to perform CRUD operations and handle user interactions.
- **Backend** interacts with **MongoDB** for data persistence and **Redis** for keeping access_tokens.
- **MongoDB** and **Redis** services are set up with persistent storage to ensure data durability.

## Docker Usage

1. Start the application by running `docker-compose up`.
2. Access the frontend application at `http://localhost:3000`.
3. The backend API can be accessed at `http://localhost:3001`.

For more details on each component, refer to the respective service documentation.
