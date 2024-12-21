# User Registration Endpoint Documentation

## Endpoint
`POST /users/register`

## Description
This endpoint is used to register a new user. It requires the user's first name, last name, email, and password. The password will be hashed before storing it in the database. Upon successful registration, a JSON Web Token (JWT) is generated and returned along with the user details.

## Request Body
The request body must be a JSON object with the following fields:

- `fullname.firstname` (string): The first name of the user. Must be at least 3 characters long.
- `fullname.lastname` (string): The last name of the user. Must be at least 3 characters long.
- `email` (string): The email address of the user. Must be a valid email format.
- `password` (string): The password for the user account. Must be at least 6 characters long.

### Example Request Body
```json
{
    "fullname": {
        "firstname": "John",
        "lastname": "Doe"
    },
    "email": "john.doe@example.com",
    "password": "password123"
}
```

## Response
### Success Response
- **Status Code:** `201 Created`
- **Content:**
    ```json
    {
        "user": {
            "_id": "user_id",
            "fullname": {
                "firstname": "John",
                "lastname": "Doe"
            },
            "email": "john.doe@example.com"
        },
        "token": "jwt_token"
    }
    ```

### Error Responses
- **Status Code:** `400 Bad Request`
    - **Content:** When validation fails
        ```json
        {
            "errors": [
                {
                    "msg": "Invalid email",
                    "param": "email",
                    "location": "body"
                },
                {
                    "msg": "First name must be at least 3 characters long",
                    "param": "fullname.firstname",
                    "location": "body"
                },
                {
                    "msg": "Password must be at least 6 characters long",
                    "param": "password",
                    "location": "body"
                }
            ]
        }
        ```

## Notes
- Ensure that the `Content-Type` header is set to `application/json` when making the request.
- The JWT token returned in the response should be stored securely on the client side for authentication in subsequent requests.
