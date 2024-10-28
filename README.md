# Password Reset Flow - Backend API

A secure backend API built with **Node.js** and **Express**, connected to **MongoDB Atlas** for storing user data. This API provides user authentication with secure password reset functionality via email verification, and includes basic CRUD operations for user data management.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [API Endpoints](#api-endpoints)
  - [User Registration](#register-user)
  - [User Login](#login-user)
  - [Password Reset Request](#request-password-reset)
  - [Password Reset Execution](#execute-password-reset)
- [Security Measures](#security-measures)
- [Setup Instructions](#setup-instructions)
- [License](#license)

---

## Project Overview

This API handles secure user registration, login, and password reset functionality. The password reset flow sends a unique, time-sensitive reset link to the user's email. This API is structured for secure data handling, password hashing, and efficient database interaction through MongoDB.

---

## Features

- **User Authentication**: Secure login and registration with password hashing.
- **Password Reset**: Email-based password reset functionality with a time-sensitive reset link.
- **CRUD Operations**: Supports basic CRUD operations for user-related data.
- **Error Handling**: Provides clear, structured responses for various error cases.
- **MongoDB Atlas Integration**: Stores user data in MongoDB Atlas, a cloud-based MongoDB solution.

---

## Technology Stack

- **Node.js & Express**: For backend server and RESTful API endpoints.
- **MongoDB Atlas**: Cloud-based storage for user data.
- **Mongoose**: ODM for MongoDB to simplify data modeling.
- **Nodemailer**: For sending password reset emails to users.
- **bcrypt**: To securely hash user passwords.
- **JWT (JSON Web Token)**: Token-based user authentication and session management.

---

## API Endpoints

### Register User

- **URL**: `/api/auth/register`
- **Method**: `POST`
- **Description**: Registers a new user and securely stores the hashed password.

#### Request Body

```json
{
  "email": "user@example.com",
  "password": "userpassword"
}
```

#### Success Response

```json
{
  "message": "User registered successfully."
}
```

#### Error Response

- **409 Conflict**: Email already exists.
  ```json
  {
    "error": "Email is already registered."
  }
  ```

---

### Login User

- **URL**: `/api/auth/login`
- **Method**: `POST`
- **Description**: Authenticates the user and returns a JWT token upon successful login.

#### Request Body

```json
{
  "email": "user@example.com",
  "password": "userpassword"
}
```

#### Success Response

```json
{
  "token": "your_jwt_token"
}
```

#### Error Response

- **401 Unauthorized**: Invalid credentials.
  ```json
  {
    "error": "Invalid email or password."
  }
  ```

---

### Request Password Reset

- **URL**: `/api/auth/request-reset`
- **Method**: `POST`
- **Description**: Sends a password reset link to the user’s registered email.

#### Request Body

```json
{
  "email": "user@example.com"
}
```

#### Success Response

```json
{
  "message": "Password reset link sent to your email."
}
```

#### Error Response

- **404 Not Found**: Email not registered.
  ```json
  {
    "error": "No user found with this email."
  }
  ```

---

### Execute Password Reset

- **URL**: `/api/auth/reset-password`
- **Method**: `POST`
- **Description**: Allows the user to set a new password using the token from the reset link.

#### Request Body

```json
{
  "token": "resetToken",
  "newPassword": "newpassword"
}
```

#### Success Response

```json
{
  "message": "Password has been reset successfully."
}
```

#### Error Response

- **400 Bad Request**: Expired or invalid token.
  ```json
  {
    "error": "The password reset link is invalid or expired."
  }
  ```

---

## Security Measures

- **Password Hashing**: All passwords are hashed with bcrypt to ensure secure storage.
- **JWT Authentication**: Each login session is token-based, providing secure, stateless authentication.
- **Time-Sensitive Reset Links**: Password reset tokens are designed to expire after a set time, enhancing security.

---

## Setup Instructions

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-repo/password-reset-api.git
   cd password-reset-api
   ```

2. **Install Dependencies**:
   ```bash
   npm install
   ```

3. **Environment Variables**:
   - Create a `.env` file in the root directory with the following variables:
     ```plaintext
     PORT=3000
     MONGO_URI=your_mongodb_connection_string
     JWT_SECRET=your_jwt_secret_key
     EMAIL_USER=your_email_address
     EMAIL_PASS=your_email_password
     RESET_TOKEN_EXPIRY=3600 # Token expiry in seconds
     ```

4. **Start the Server**:
   ```bash
   npm start
   ```

5. **Test the API**:
   - Use Postman to test each endpoint using the example requests.

---

## License

This project is licensed under the MIT License.