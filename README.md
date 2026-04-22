🔗 **Central Documentation:** [https://github.com/fitforge101/fitforge-app-docs](https://github.com/fitforge101/fitforge-app-docs)

# Auth Service

## Overview
The `auth-service` manages user registration, secure authentication, and JSON Web Token (JWT) issuance. It serves as the primary security gateway, providing a token verification endpoint used by all other internal microservices to validate incoming requests.

## Features
*   Secure user signup with bcrypt password hashing.
*   Login endpoint issuing stateless JWTs.
*   Internal endpoint for robust JWT validation across the platform.

## Tech Stack
*   Node.js 20-slim
*   Express.js
*   MongoDB (Mongoose)
*   jsonwebtoken
*   bcryptjs

## API Endpoints
*   `POST /auth/signup` - Register a new user
*   `POST /auth/login` - Authenticate and receive JWT
*   `POST /auth/verify` - Internal token validation

## Example Request/Response

**POST `/auth/login`**
*Request:*
```json
{
  "email": "user@example.com",
  "password": "securepassword123"
}
```
*Response:*
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "userId": "64a1b2c3d4e5f67890123456",
  "name": "Jane Doe"
}
```

## Setup Instructions
1.  **Install Dependencies:**
    ```bash
    npm ci
    ```
2.  **Run Development Server:**
    ```bash
    npm run dev
    ```

## Environment Variables
*   `PORT` (Default: `5001`)
*   `MONGO_URI` (Default: `mongodb://mongo:27017/auth_db`)
*   `JWT_SECRET` (Default: `fitforge_dev_secret`)

## Folder Structure
```text
.
├── Dockerfile
├── package.json
└── src/
    ├── index.js
    ├── middleware/
    │   └── verifyToken.js
    ├── models/
    │   └── User.js
    └── routes/
        └── auth.js
```

## Deployment
This service includes a production-ready `Dockerfile` built on `node:20-slim` running as a non-root user. It is deployed via Kubernetes using the Helm charts located in the `fitforge-charts` repository.