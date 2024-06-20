# Custom Error Types in JavaScript

* Overview
Creating custom error types in JavaScript helps with more specific and informative error handling. This is achieved by extending built-in error classes to inherit and extend their functionality

* Steps to Create A Custom Error Class

1. Define the Class
    • Use the `class` keyword and extend a built-in error class (like `Error`, `SyntaxError`, etc.) using the `extends` keyword
    • Example: `class CustomError extends Error`

2. Define the Constructor
    • The constructor can take custom parameters
    • Use `super(...params)` to pass parameters to the parent class's constructor

    • Example:
    ```js
    constructor(fieldName = 'field', ...params) {
        super(...params);
        // additional code
    }
    ```

3. Capture the Stack Trace
    • Use `Error.captureStackTrace(this, ClassNameHere)` to ensure the stack trace points to the correct error location

    • Example:
    ```js
    if (Error.captureStackTrace) {
        Error.captureStackTrace(this, CustomError);
    }
    ```

4. Set the Name and Message
    • Set the `name` property to the class name
    • Customise the `message` property as needed

    • Example:
    ```js
    this.name = `CustomError`;
    this.message = `Custom error message with ${fieldName}`;
    ```
