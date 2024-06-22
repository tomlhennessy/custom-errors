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
    this.name = 'CustomError';
    this.message = `Custom error message with ${fieldName}`;
    ```

* Example 1: Basic Custom Error
```js
class SearchSyntaxError extends SyntaxError {
    constructor(...params) {
        super(...params);
        if (Error.captureStackTrace) {
            Error.captureStackTrace(this, SearchSyntaxError);
        }
        this.name = 'SearchSyntaxError';
    }
}
```

* Example 2: Custom Error with Additional Information
```js
class MissingRequiredFieldError extends Error {
    constructor(fieldName = 'field', ...params) {
        super(...params);
        if(Error.captureStackTrace) {
            Error.captureStackTrace(this, MissingRequiredFieldError);
        }
        this.name = 'MissingRequiredFieldError';
        this.fieldName = fieldName;
        this.message = `Missing required field "${fieldName}".`;
        this.date = new Date();
    }
}
```

* Using the Custom Error
```js
try {
    throw new MissingRequiredFieldError(`email`);
} catch(e) {
    console.error(e.name);      // MissingRequiredFieldError
    console.error(e.fieldName); // email
    console.error(e.message);   // Missing required field "email"
    console.error(e.stack);     // stack trace
}
```

* Summary
    • Custom error classes help create more specific error types
    • Inheritance from built-in error classes allows reuse of existing functionality
    • Constructor customisation enables additional debugging information
    • Proper stack trace and name setting are crucial for debugging

Using custom error types makes code more rebust and easier to debug, providing more context-specific error messages


# ES5 Classes

* Why Learn ES5?
    • Legacy Code: Many existing projects and libraries use ES5 syntax. Understanding ES5 ensures you can read, maintain, and update older codebases
    • Browser Compatibility: ES5 is widely supported across all browsers, including older versions. This is crucial for projects needing to support a broad range of users.

* Creating a Class Constructor Function

    In ES5, classes are created using constructor functions
    ```js
    function Book(title, series, author) {
        this.title = title;
        this.series = series;
        this.author = author;
    }

    const gobletOfFire = new Book('The Goblet of Fire', 'Harry Potter', 'J.K. Rowling');
    console.log(gobletOfFire.title); // The Goblet of Fire
    ```
    • Constructor Function: A Function used to create instances of a class
    • `new` Keyword: Used to create a new instance of the class
    • `this` Keyword: Refers to the newly created object instance


* Static Methods and Variables

    Static methods and variables are added directly to the constructor function:
    ```js
    Book.getTitles = function(...books) {
        return books.map(book => book.title);
    }

    Book.genres = ['fantasy', 'horror', 'classics', 'mystery'];

    const titles = Book.getTitles(gobletOfFire);
    console.log(titles); // ['The Goblet of Fire']
    console.log(Book.genres); // ['fantasy', 'horror', 'classics', 'mystery']
    ```
    • Static Method: A method that belongs to the class itself, not the instance
    • Static Variable: A variable that belongs to the class itself


* Instance Methods

Instance Methods are added to the prototype of the constructor function

    ```js
    Book.prototype.toString = function() {
        return `${this.title} by ${this.author}`;
    }

    console.log(gobletOfFire.toString()); // The Goblet of Fire by J.K. Rowling
    ```
    • Instance Method: A method that belongs to the instance of the class
    • Prototype: An object from which other objects inherit properties


* Monkey-Patching

Monkey-patching involves modifying or extending existing classes after they have been defined:

    ```js
    String.prototype.helloWorld = function() {
        console.log("hello World!");
    }

    const str = "";
    str.helloWorld(); // prints "Hello World!"
    ```
    • Monkey-Patching: Adding or modifying methods and properties of existing classes, often used for built-in classes like `String`, `Array`, and `Object`


* Summary
    • Constructor Function: Create classes using functions with the `new` keyword
    • Static Methods and Variables: Attach directly to the constructor function
    • Instance Methods: Attach to the prototype of the constructor function
    • Monkey-Patching: Modify existing classes to add or override methods
