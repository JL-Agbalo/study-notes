# Server Side Session Management

- https://www.youtube.com/watch?v=U6OcC0yq1CE&t

# TODO continue

## Login Page

The login page where users enter their credentials to access the application.

## POST /login

Endpoint to handle user login requests.

```json
{
  "email": "sample@gmail.com",
  "password": "password"
}
```

## HTTP Only Secure Cookie with Session ID

A secure cookie that is only accessible via HTTP, used to store the session ID.

## Server

The backend server that handles session management.

## Session Secret

A secret key used by the server to sign and verify session IDs.

## PostgreSQL

A relational database used to store user data and session information.

## Create Session Store (e.g., Redis)

A session store like Redis is used to manage and persist session data.
