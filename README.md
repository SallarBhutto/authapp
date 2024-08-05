# Application Overview
Easygenerator Auth app task

**Notes:**
- All secrets, such as database credentials and API keys, should be securely stored in a KeyVault rather than hard-coded in configuration files.

## Table of Contents

1. [Main Repository](#main-repository)
2. [Components](#components)
   - [Frontend](#frontend)
   - [Backend](#backend)
   - [MongoDB](#mongodb)
   - [Redis](#redis)
3. [Workflow](#workflow)
4. [Docker Usage](#docker-usage)
4. [Local Setup](#local-setup)

## Main Repository

- **Repository Name**: authapp
- **Description**: The main repository for the Auth App project, which includes submodules for frontend and backend services.
- **frontend**: https://github.com/SallarBhutto/frontend
- **backend**: https://github.com/SallarBhutto/backend

## Components

The application consists of four main components:

1. **Frontend**
   - **Description**: A React-based frontend application that serves the user interface. It is designed to communicate with the backend service to Sign-up and Sign-in the user.
   - **Key Dependencies**:
   - `@emotion/react`, `@emotion/styled`: For styling and theming.
   - `@mui/material`: Material-UI components for building the UI.
   - `axios`: For making HTTP requests.
   - `react`, `react-dom`: Core React libraries.
   - `react-router-dom`: For routing and navigation.
   - `typescript`: For type safety.
   - **Port**: Exposed on port 3000.
   - **Environment Variable**:
     - `REACT_APP_API_BASE_URL`: Points to the backend service URL.

2. **Backend**
   - **Description**: A NestJS-based backend application that handles business logic, user authentication, and data management. It connects to both MongoDB and Redis for persistent storage and caching.
   - **Key Dependencies**:
   - `@nestjs/common`, `@nestjs/core`: Core NestJS libraries for building the application.
   - `@nestjs/jwt`: For JWT authentication.
   - `@nestjs/mongoose`: For MongoDB integration.
   - `ioredis`: For Redis integration.
   - `bcrypt`: For password hashing.
   - `class-validator`: For validating input data.
   - `cookie-parser`: For handling cookies.
   - `mongoose`: For MongoDB data modeling.
   - `passport`, `passport-jwt`: For authentication strategies.
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


- **Authentication**:
  - The **Frontend** sends login or signup credentials to the **Backend**.
  - The **Backend** validates the credentials or creates a new user.
  - Upon successful authentication, the **Backend** sets an HTTP-only cookie containing the access token, which is sent to the **Frontend**. This cookie is used for maintaining user sessions securely.
- **Frontend** communicates with the **Backend** to perform CRUD operations and handle user interactions.
- **Backend** interacts with **MongoDB** for data persistence and **Redis** for keeping access_tokens.
- **MongoDB** and **Redis** services are set up with persistent storage to ensure data durability.

## Docker Usage

1. Start the application by running `docker-compose up` or `docker-compose up -d` for detach mode.
2. Access the frontend application at `http://localhost:3000`.
3. The backend API can be accessed at `http://localhost:3001`.

### Services

- **MongoDB**: Stores application data and is initialized with root credentials and a default database.
- **Redis**: Provides caching and session storage.
- **Frontend**: Serves the React application and connects to the backend service.
- **Backend**: Runs the NestJS application, connects to MongoDB for data storage, and uses Redis for caching.

### Troubleshooting

If you encounter the `invalid ELF header` error on backend container, which is often caused by a mismatch between the environment where the module(bycrpt) was installed and where it is being run, follow these steps to resolve the issue:

1. Remove existing `node_modules` and `package-lock.json` files in the backend directory:
    ```bash
    rm -rf backend/node_modules backend/package-lock.json
    ```

2. Stop and remove Docker volumes:
    ```bash
    docker-compose down --volumes
    ```

3. Rebuild Docker images without using cache:
    ```bash
    docker-compose build --no-cache
    ```

4. Start Docker containers in detached mode:
    ```bash
    docker-compose up -d
    ```

## Local Setup

1. Clone the main repository and initialize the submodules:

    ```bash
    git clone --recurse-submodules https://github.com/SallarBhutto/authapp.git
    ```

2. Navigate into the project directory:

    ```bash
    cd AuthApp
    ```

3. Install dependencies for both frontend and backend:

    ```bash
    # For frontend
    cd frontend
    npm install

    # For backend
    cd ../backend
    npm install
    ```

4. Set up MongoDB and Redis locally. You can use the official Docker images or install them directly on your machine.

   - **MongoDB**: Follow the [MongoDB installation guide](https://docs.mongodb.com/manual/installation/) for your operating system.
   - **Redis**: Follow the [Redis installation guide](https://redis.io/download) for your operating system.

5. Create a `.env` file in the `backend` directory and add the necessary environment variables:

    ```env
    MONGO_URI=mongodb://root:example@localhost:27017/mongodb?authSource=admin
    JWT_SECRET=secret_key
    REDIS_HOST=localhost
    REDIS_PORT=6379
    ```

6. Start MongoDB and Redis services:

   - **MongoDB**:
     ```bash
     mongod --dbpath /path/to/your/data/db
     ```
   
   - **Redis**:
     ```bash
     redis-server
     ```

7. Run the backend server:

    ```bash
    # In the backend directory
    npm run start:dev
    ```

8. Run the frontend server:

    ```bash
    # In the frontend directory
    npm start
    ```
9. **Run Tests for Frontend and Backend**

   - **Frontend (React)**:
     1. Navigate to the `frontend` directory:
        ```bash
        cd frontend
        ```
     2. Run the tests:
        ```bash
        npm test
        ```
     3. To run tests in watch mode (automatically re-runs tests on file changes):
        ```bash
        npm test -- --watch
        ```

   - **Backend (NestJS)**:
     1. Navigate to the `backend` directory:
        ```bash
        cd ../backend
        ```
     2. Run the tests:
        ```bash
        npm test
        ```
     3. To run tests with watch mode (automatically re-runs tests on file changes):
        ```bash
        npm run test:watch
        ```

10. Access the frontend application at `http://localhost:3000`.

11. The backend API can be accessed at `http://localhost:3001`.

## Local Setup Notes

- Ensure that MongoDB and Redis are running and accessible on the configured ports.
- Adjust the `.env` configuration based on your local setup and security requirements.
- Verify that the required ports are open and not used by other applications.

Thank you!
