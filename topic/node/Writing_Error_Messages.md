
---

**Filename:** `Writing_Error_Messages.md`

---

# Writing Error Messages

**Purpose**: This guide provides best practices for writing clear, structured, and actionable error messages in Node.js applications, with an emphasis on consistent error handling and helpful feedback for users and developers.

---

## Writing Error Messages

### 1. Structure for Clarity
   - **Consistency in Error Messages**: Standardize the format of error messages to make them predictable and easy to interpret. Each error message should include:
      - A concise description of the error.
      - An optional status code (for HTTP responses).
      - Additional contextual information if available.
   - **Example**:
     ```typescript
     const error = {
       message: "Invalid request format",
       statusCode: 400,
       info: "Expected 'username' field in request body",
     };
     ```
   - **Why It’s Important**: Consistent error structures allow developers and users to quickly understand the issue and possible steps for resolution.
   - **Further Reading**:
      - [Error Handling in Node.js](https://nodejs.dev/learn/error-handling-in-nodejs)

### 2. Using Interfaces for Error Structuring
   - **Define Error Interfaces in TypeScript**: Use interfaces to define a standard structure for error objects, making error properties optional where applicable to avoid excessive verbosity.
   - **Example**:
     ```typescript
     interface AppError {
       message: string;
       statusCode?: number;
       details?: string;
     }

     const error: AppError = {
       message: "User not found",
       statusCode: 404,
     };
     ```
   - **Why It’s Useful**: By structuring errors with interfaces, you ensure consistent properties across all error messages, making the codebase more predictable and easier to debug.
   - **Further Documentation**:
      - [TypeScript Optional Properties](https://www.typescriptlang.org/docs/handbook/interfaces.html#optional-properties)

### 3. Avoiding Technical Jargon
   - **Clear Language**: Avoid using technical jargon in error messages. Keep messages straightforward so that non-technical users can understand the issue.
   - **Example**:
     ```typescript
     // Less clear
     message: "Authentication token validation failed due to misconfiguration."
     
     // More user-friendly
     message: "Invalid token. Please log in again."
     ```
   - **Why It’s Important**: Simple language improves the user experience and reduces confusion, especially for end-users who may not be familiar with technical terminology.

### 4. Provide Actionable Advice
   - **Suggest Next Steps**: Where possible, error messages should provide a hint or a suggested action to resolve the issue.
   - **Example**:
     ```typescript
     const error = {
       message: "Password too short",
       statusCode: 400,
       suggestion: "Use at least 8 characters for your password",
     };
     ```
   - **Why It’s Useful**: Actionable advice reduces frustration by guiding users on how to fix the error themselves, resulting in a smoother user experience.
   - **Further Reading**:
      - [Designing User-Friendly Error Messages](https://uxdesign.cc/designing-error-messages-c7d9d0d70f7)

### 5. Log Detailed Errors, Display General Messages
   - **Separation of User and Developer Messages**: Log the full error details for debugging while displaying a simplified error message to the user to avoid revealing sensitive information.
   - **Example**:
     ```typescript
     // Logged error
     console.error("Database connection failed:", error);

     // User-facing error
     res.status(500).json({ message: "An unexpected error occurred. Please try again later." });
     ```
   - **Why It’s Important**: This practice improves security by hiding internal details from users while still providing valuable information in logs for debugging.
   - **Further Documentation**:
      - [Logging Best Practices in Node.js](https://nodejs.dev/learn/how-to-log-an-object-in-nodejs)

### 6. Use HTTP Status Codes in Node.js
   - **HTTP Status Codes**: Use appropriate HTTP status codes for error responses in API applications. This provides an additional layer of information for clients interacting with the API.
      - **400**: Bad Request (client-side input error).
      - **401**: Unauthorized (authentication issue).
      - **404**: Not Found (requested resource missing).
      - **500**: Internal Server Error (server issue).
   - **Example**:
     ```typescript
     res.status(404).json({ message: "Resource not found" });
     ```
   - **Further Reading**:
      - [HTTP Status Codes Reference](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

### 7. Catching and Re-throwing Errors with Context
   - **Error Wrapping**: When catching an error, add context before re-throwing it to provide more information about where and why the error occurred.
   - **Example**:
     ```typescript
     try {
       await databaseConnect();
     } catch (error) {
       throw new Error(`Database connection failed: ${error.message}`);
     }
     ```
   - **Why It’s Important**: Adding context to errors improves traceability, making it easier to locate the source of an issue.

### 8. Localize User-Facing Error Messages (if Applicable)
   - **Localization for Multilingual Apps**: For applications that support multiple languages, provide translated error messages to improve accessibility and user experience for a global audience.
   - **Example**:
     ```typescript
     const errors = {
       en: { message: "Invalid credentials" },
       es: { message: "Credenciales no válidas" },
     };
     ```
   - **Why It’s Useful**: Localized error messages make applications more user-friendly and accessible, especially for non-English-speaking users.
   - **Further Reading**:
      - [Localization in JavaScript Applications](https://phrase.com/blog/posts/ultimate-guide-to-javascript-localization-i18n/)

