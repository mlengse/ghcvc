---
applyTo: "**/*.kt,**/*.kts"
---
# Kotlin Style Guide

## Naming Conventions
- Use camelCase for variables, functions, and properties
- Use PascalCase for classes, interfaces, and objects
- Use SCREAMING_SNAKE_CASE for constants
- Use backticks for identifiers with spaces or keywords
- Prefix interface names with 'I' is not recommended
- Use descriptive, meaningful names

## Formatting
- Use 4 spaces for indentation
- Keep line length reasonable (typically 100-120 characters)
- Use ktlint or detekt for automated formatting
- Place opening braces on the same line
- Add spaces around binary operators
- Use trailing commas in multi-line parameter lists
- Format multiline functions and classes consistently

## Language Features
- Prefer val over var when possible
- Use extension functions to extend functionality
- Use data classes for model classes
- Use sealed classes for representing restricted hierarchies
- Use object declarations for singletons
- Use companion objects for factory methods and static members
- Use type aliases to simplify complex types
- Use lambdas and higher-order functions where appropriate
- Leverage null safety features with proper nullability annotations
- Use smart casts when possible
- Prefer property delegation over manual implementation

## Collections
- Use the collection factory functions (listOf, mapOf, setOf)
- Use the scope functions (let, run, with, apply, also) appropriately
- Use collection transformations (map, filter, reduce) over loops
- Use sequences for large collections to improve performance
- Use inline functions with reified generics when needed

## Coroutines
- Use suspending functions for asynchronous operations
- Apply appropriate coroutine scope for lifecycle management
- Use structured concurrency patterns
- Handle exceptions in coroutines properly
- Use appropriate dispatchers for different types of work
- Apply flow for reactive streams

## Android-Specific (if applicable)
- Use ViewModel for UI-related data storage and business logic
- Use LiveData or Flow for observable data
- Apply proper coroutine scopes (viewModelScope, lifecycleScope)
- Use view binding or data binding instead of findViewById
- Implement dependency injection with Hilt or Koin
- Apply the repository pattern for data operations

## Testing
- Use JUnit for unit testing
- Use MockK for mocking dependencies
- Test coroutines using TestDispatcher
- Use runTest for testing suspending functions
- Test viewmodels with InstantTaskExecutorRule
- Write instrumentation tests for Android components

## Documentation
- Document public APIs with KDoc comments
- Include examples in documentation
- Document nullable parameters and return values
- Explain complex algorithms or business rules
- Use @throws to document exceptions
