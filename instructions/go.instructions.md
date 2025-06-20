---
applyTo: "**/*.go"
---
# Go Style Guide

## Naming Conventions
- Use MixedCaps (camelCase) for exported names
- Use mixedCaps for non-exported names
- Use short, descriptive names
- Acronyms should be all uppercase (e.g., HTTP, URL, ID)
- Interface names often end with -er (e.g., Reader, Writer)

## Formatting
- Use gofmt for automated code formatting
- Indent with tabs, not spaces
- Keep line lengths reasonable (under 120 characters)
- Group related declarations together
- Add empty lines between function definitions

## Error Handling
- Check errors explicitly; don't use try-catch patterns
- Return errors rather than using exceptions
- Use the fmt.Errorf function for formatting error messages
- Create custom error types for specific error cases when needed
- Consider using errors.Is() and errors.As() for error inspection

## Best Practices
- Follow the Go Proverbs (https://go-proverbs.github.io/)
- Prefer composition over inheritance
- Use interfaces for decoupling
- Make zero values useful
- Use context.Context for cancellation, timeouts, and passing request-scoped values
- Use goroutines and channels appropriately
- Avoid global variables
- Implement proper resource cleanup with defer

## Concurrency
- Use goroutines for concurrent operations
- Use channels for communication between goroutines
- Consider sync primitives (Mutex, RWMutex) for simple shared state
- Avoid data races by proper synchronization
- Be cautious with goroutine leaks
- Use context for cancellation

## Testing
- Write table-driven tests
- Use subtests for organizing test cases
- Use t.Helper() for helper functions
- Use go test's built-in features like test coverage
- Use testify or other assertion libraries sparingly
- Consider benchmarks for performance-critical code
- Use examples that serve as documentation
