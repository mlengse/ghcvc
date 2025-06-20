---
applyTo: "**/*.dart,**/flutter/**"
---
# Flutter Style Guide

## Architecture
- Prefer a clear architectural pattern (BLoC, Provider, Redux, MVC, etc.)
- Separate UI, business logic, and data layers
- Use dependency injection for better testability
- Create reusable widgets for common UI patterns
- Organize code by feature/module when possible

## State Management
- Choose an appropriate state management solution for the complexity of the app
- For simple state, use setState or Provider
- For complex state, consider BLoC, Riverpod, or other solutions
- Keep state management logic separate from the UI code
- Minimize state duplication across the app

## Widget Structure
- Split large widgets into smaller, reusable components
- Use StatelessWidget when possible
- Override the operator == and implement hashCode for Widget keys
- Keep build methods simple and focused
- Extract complex build logic into helper methods
- Add comments for widget sections and complex layout arrangements

## Performance
- Use const constructors for widgets that don't change
- Implement shouldRepaint and shouldRebuild when appropriate
- Use ListView.builder for long lists
- Avoid expensive operations in the build method
- Use RepaintBoundary to limit UI updates
- Consider using cached_network_image for network images
- Optimize asset sizes and formats

## UI Design
- Follow Material Design or Cupertino guidelines when appropriate
- Use ThemeData for consistent styling
- Extract text styles, colors, and dimensions into theme or constant files
- Use MediaQuery for responsive layouts
- Implement proper dark mode support
- Ensure proper handling of different screen sizes and orientations
- Use SizedBox or Container for spacing rather than Padding when appropriate

## Navigation
- Use named routes for better maintainability
- Consider using a router package for complex navigation requirements
- Handle deep links properly
- Use appropriate transitions between screens
- Implement proper back button handling

## Testing
- Write widget tests for UI components
- Create unit tests for business logic
- Use integration tests for critical user flows
- Mock external dependencies and services
- Test edge cases and error scenarios

## Accessibility
- Use semantic labels for important widgets
- Handle text scaling for users with vision impairments
- Use sufficient color contrast for text
- Ensure touch targets are at least 48x48 pixels
- Test with screen readers and other accessibility tools
