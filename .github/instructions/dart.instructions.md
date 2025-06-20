---
applyTo: "**/*.dart"
---
# Dart Style Guide

## Naming Conventions
- Use lowerCamelCase for variables, functions, and methods
- Use UpperCamelCase for classes, enum types, typedefs, and extensions
- Use lowercase_with_underscores for libraries, packages, directories, and files
- Prefix private identifiers with underscore (_)
- Use SCREAMING_CAPS for constants

## Formatting
- Use 2 spaces for indentation
- Limit lines to 80 characters when possible
- Use dartfmt (dart format) for consistent formatting
- Place the opening curly brace on the same line
- Add spaces between control flow keywords and parentheses
- Always use curly braces for control flow statements, even for single-line bodies

## Best Practices
- Prefer final for variables that don't change
- Use const for compile-time constants
- Make fields private unless they need to be accessed from outside
- Use getters/setters instead of public fields when behavior might change
- Avoid using dynamic unless necessary
- Use collection literals instead of constructors
- Use cascades (..) to chain operations on the same object
- Use async/await for asynchronous code instead of raw Futures
- Use named parameters for greater clarity, especially for boolean flags

## Collections
- Use collection literals instead of constructors
- Use the spread operator (...) and collection if when appropriate
- Use const for compile-time constant collections
- Consider using more specialized collections like queues or sets when appropriate

## Error Handling
- Use try-catch blocks for expected exceptions
- Return Futures that complete with errors for asynchronous failures
- Avoid catching exceptions without handling them
- Be explicit about error types when possible

## Asynchronous Programming
- Prefer async/await over using raw Futures
- Mark functions that return Futures as async
- Handle errors in async code using try-catch or catchError
- Use Future.wait for parallel operations
- Consider using Streams for event sequences

## Testing
- Write unit tests using the test package
- Use descriptive test names
- Group related tests with group()
- Mock dependencies for isolation
- Test edge cases and error scenarios
