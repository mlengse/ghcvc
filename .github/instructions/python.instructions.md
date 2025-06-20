---
applyTo: "**/*.py"
---
# Python Style Guide

## Naming Conventions
- Use snake_case for variables and functions
- Use PascalCase for classes
- Use UPPER_CASE for constants
- Prefix private members with underscore (_)

## Formatting
- Follow PEP 8 guidelines
- Use 4 spaces for indentation
- Keep line lengths below 88 characters (Black formatter standard)
- Use double quotes for strings consistently

## Imports
- Organize imports in three blocks: standard library, third-party packages, local modules
- Sort imports alphabetically within each block
- Avoid wildcard imports (from module import *)
- Prefer absolute imports over relative imports

## Best Practices
- Use type hints for function parameters and return values
- Write docstrings for all public functions, classes, and modules
- Use context managers (with statement) for resource management
- Follow the principle of "explicit is better than implicit"
- Use list/dict/set comprehensions when appropriate
- Prefer built-in functions and standard library solutions

## Error Handling
- Use specific exception types
- Only catch exceptions you can handle
- Use finally blocks for cleanup
- Prefer context managers for resource management

## Testing
- Use pytest for unit testing
- Write small, focused test functions
- Use descriptive test function names
- Use fixtures to set up test data
- Parameterize similar tests
