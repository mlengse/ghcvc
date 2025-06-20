---
applyTo: "**/*.rs"
---
# Rust Style Guide

## Naming Conventions
- Use snake_case for variables, functions, and modules
- Use PascalCase for types, traits, and enum variants
- Use SCREAMING_SNAKE_CASE for statics and constants
- Use descriptive names that reflect purpose
- Prefer concise but clear names

## Formatting
- Use the standard Rust formatting via rustfmt
- Use 4 spaces for indentation
- Limit lines to 100 characters when possible
- Place opening brackets on the same line
- Use spaces around binary operators

## Error Handling
- Use Result<T, E> for operations that might fail
- Use Option<T> for values that might not exist
- Avoid unwrap() and expect() in production code
- Implement proper error types with std::error::Error
- Use the ? operator for error propagation
- Consider using thiserror or anyhow for error management
- Add context to errors when propagating them

## Ownership and Borrowing
- Prefer borrowing over ownership when possible
- Use &str over String when you only need to read
- Use references with appropriate lifetimes
- Avoid unnecessary clones
- Use Cow<'a, T> when you need to decide between borrowing and owning at runtime
- Be explicit about lifetimes when necessary

## Memory Safety
- Avoid unsafe code unless absolutely necessary
- Document all unsafe blocks extensively
- Encapsulate unsafe code in safe abstractions
- Use checked arithmetic operations to prevent overflows
- Consider using types like NonZeroU32 when applicable
- Validate external input thoroughly

## Modules and Organization
- Use the module system to organize code logically
- Keep public APIs minimal and well-documented
- Use private implementation details when possible
- Place tests in a tests module with the #[cfg(test)] attribute
- Use feature flags for optional functionality

## Concurrency
- Use message passing with channels when possible
- Use mutexes and other sync primitives when appropriate
- Avoid data races with proper synchronization
- Consider using the rayon crate for parallel operations
- Implement Send and Sync traits appropriately
- Document thread safety guarantees

## Type System
- Use Rust's type system to prevent bugs at compile-time
- Use enums for representing different states or variants
- Implement proper traits for your types
- Use generics for code reuse
- Use associated types to simplify complex generics
- Leverage type-level programming when beneficial

## Documentation
- Document all public APIs with rustdoc comments
- Include examples in documentation
- Document panicking conditions
- Use markdown formatting in doc comments
- Run doctests to ensure documentation is correct

## Testing
- Write unit tests for functions and methods
- Use #[test] attribute for test functions
- Use assert!, assert_eq!, and assert_ne! macros
- Write integration tests in the tests/ directory
- Use property-based testing when applicable
- Benchmark performance-critical code
