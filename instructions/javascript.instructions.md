---
applyTo: "**/*.js,**/*.jsx,**/*.ts,**/*.tsx"
---
# JavaScript and TypeScript Style Guide

## Naming Conventions
- Use camelCase for variables and functions
- Use PascalCase for classes and React components
- Use UPPER_CASE for constants
- Prefix private class fields with underscore (_)

## TypeScript Specifics
- Always provide explicit types for function parameters and return types
- Use interfaces for object shapes and types for unions/intersections
- Prefer type safety over any types
- Use unknown over any when possible

## Formatting
- Use 2 spaces for indentation
- Use semicolons at the end of statements
- Keep line lengths below 100 characters
- Use single quotes for strings

## Best Practices
- Use async/await over Promises and callbacks when possible
- Use const for variables that don't change
- Prefer destructuring for objects and arrays
- Use spread operators for shallow copies
- Use optional chaining and nullish coalescing
- Prefer functional approaches like map, filter, reduce over imperative loops

## React Recommendations
- Use functional components with hooks
- Break UI into small, reusable components
- Manage component state appropriately
- Avoid inline styles when possible
- Use memo and useMemo for performance optimization

## Testing
- Use Jest for testing framework
- Test components with React Testing Library
- Mock external dependencies
- Focus on testing behavior, not implementation details
