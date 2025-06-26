---
mode: "agent"
description: "Create a new API endpoint"
---
# Create a New API Endpoint

Create a new API endpoint with the following characteristics:

1. **Endpoint Definition**:
   - Define the HTTP method (GET, POST, PUT, DELETE, etc.)
   - Define the route path and any path parameters
   - Define query parameters if applicable
   - Define request body schema if applicable

2. **Input Validation**:
   - Validate all input parameters
   - Handle malformed input gracefully

3. **Authentication & Authorization**:
   - Apply appropriate authentication middleware
   - Implement authorization checks

4. **Business Logic**:
   - Implement the required functionality
   - Make necessary database queries or external API calls
   - Handle edge cases and error scenarios

5. **Response**:
   - Define appropriate status codes
   - Structure the response body according to API conventions
   - Include proper error messages when needed

6. **Documentation**:
   - Add API documentation comments
   - Document request/response formats
   - Include example usage

7. **Testing**:
   - Create unit tests for the endpoint
   - Add integration tests if appropriate

Follow RESTful principles and the existing API structure of the project. Ensure proper error handling and security practices.
