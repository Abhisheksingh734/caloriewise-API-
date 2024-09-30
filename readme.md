# CalorieWise API

A simple RESTful API for managing users, food data, and tracking food consumption.

## Table of Contents

- [Installation](#installation)
- [Project Structure](#project-structure)
- [Features](#features)
- [Endpoints](#endpoints)
- [Models](#models)
- [Authentication](#authentication)
- [Usage](#usage)
- [License](#license)

## Installation

1. Clone the repository:
   
    ```bash
    git clone https://github.com/yourusername/caloriewise-api.git
    ```
2. Navigate to the project directory:
   
    ```
    cd caloriewise-api
    ```
3. Install the necessary packages:
   
    ```
    npm install
    ```

4. Run the application:

    ```
    npm start
    ```

## Project Structure
```
.
├── models
│   ├── userModel.js
│   ├── foodModel.js
│   └── trackingModel.js
├── index.js
├── verifyToken.js
└── README.md
```

- `models/` - Contains Mongoose schemas for `User`, `Food`, and `Tracking`.
- `index.js` - The main application file, defining routes and initializing the Express server.
- `verifyToken.js` - Middleware for verifying JWT authentication tokens.
  

## Features
- User authentication with JWT (Register and Login)
- Food tracking system
- Secure API endpoints requiring authentication for tracking and retrieving food data
- Mongoose ORM for database operations


## Endpoints

### 1. User Registration
  - POST `/user`
  - Registers a new user.
  - Request Body
    ```
     {
         "name": "John Doe",
         "email": "john@example.com",
         "password": "password123",
         "age": 25
      };
    ```

### 2. User login
  - POST `/login`
  - Logs in a user and returns a JWT token.
  - Request Body
    ```
     {
        "email": "john@example.com",
        "password": "password123"
     }
    ```

### 3. Get All Foods
  - GET `/foods` (Requires JWT)
  - Returns a list of all available foods.

### 4. Search Food by Name
  - GET `/foods/:name` (Requires JWT)
  - Searches for a food by name (case-insensitive).

### 5. Track Food Consumption
  - POST `/track` (Requires JWT)
  - Tracks food consumption for a user.
  - Request Body
    ```
     {
        "userId": "USER_ID_HERE",
        "foodId": "FOOD_ID_HERE",
        "quantity": 2
     }
    ```
### 6. Get Tracked Foods by User and Date
  - GET `/track/:userId/:date` (Requires JWT).
  - Retrieves all foods tracked by a user on a specific date.


## Models

### 1. User Model
  - Fields: `name`, `email`, `password`, `age`
  - Password is hashed using bcryptjs for security.
### 3. Food Model
  - Fields: `name`, `calories`, `protein`, `fat`, `fiber`, `carbohydrates`
  - Stores nutritional information for each food item.
### 4. Tracking Model
  - Fields: `userId`, `foodId`, `eatenDate`, `quantity`
  - Tracks when a user eats a food item, its quantity, and on what date.

## Authentication 
This API uses JSON Web Tokens (JWT) for authentication. After logging in, you will receive a token, which you must include in the headers of subsequent requests to protected endpoints.

#### Usage of JWT
In protected routes, you need to pass the token in the Authorization header like this:
  ```
    Bearer <AuthToken-from-login>
  ```
To validate tokens, the middleware `verifyToken` is used.

### Usage
- Register a new user via the `/register` endpoint.
- Login with the registered user via `/login` to receive a JWT token.
- Use the token to access protected routes like `/foods`, `/track`, and `/track/:userId/:date`.


## License
  This project is licensed under the MIT License.
