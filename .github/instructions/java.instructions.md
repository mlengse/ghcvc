---
applyTo: "**/*.java"
---
# Java Style Guide

## Naming Conventions
- Use camelCase for variables and methods
- Use PascalCase for classes and interfaces
- Use UPPER_SNAKE_CASE for constants
- Package names should be all lowercase

## Formatting
- Use 4 spaces for indentation
- Keep line lengths below 120 characters
- Use braces even for single-line blocks
- Place opening braces on the same line
- Add a space after keywords like if, for, while

## Best Practices
- Favor composition over inheritance
- Make fields private and provide getters/setters as needed
- Use interfaces to define contracts
- Minimize method visibility (private, package-private, protected, public)
- Use meaningful exception names and messages
- Prefer immutable objects when possible
- Use streams and functional programming when appropriate

## Exception Handling
- Use specific exception types
- Document exceptions in Javadoc
- Don't catch Exception unless necessary
- Don't swallow exceptions (empty catch blocks)
- Use try-with-resources for AutoCloseable resources

## Java Collections
- Use interface types in declarations (List instead of ArrayList)
- Prefer the Collections Framework over arrays
- Use generics to provide type safety
- Consider using immutable collections when appropriate

## Concurrency
- Minimize shared mutable state
- Use java.util.concurrent classes instead of raw synchronization
- Document thread safety for classes designed for concurrent use
- Be aware of memory consistency effects

## Testing
- Use JUnit for unit testing
- Mock dependencies with Mockito
- Test edge cases and error scenarios
- Follow the AAA pattern (Arrange, Act, Assert)
