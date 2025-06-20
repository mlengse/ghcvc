---
applyTo: "**/*.jsx,**/*.tsx,**/*react*/**"
---
# React Style Guide

## Component Structure
- Use functional components with hooks rather than class components
- Keep components small and focused on a single responsibility
- Split large components into smaller, reusable ones
- Use PascalCase for component names and camelCase for instances
- Place each component in its own file when appropriate
- Group related components in directories

## Props
- Use prop destructuring in function parameters
- Define prop types with PropTypes or TypeScript
- Set default values for optional props
- Avoid excessive prop drilling; consider context or state management
- Use spread operator for props when appropriate, but be mindful of overuse
- Pass callbacks as props, not inline functions, to avoid unnecessary rerenders

## State Management
- Use useState for simple component state
- Use useReducer for complex state logic
- Consider external state management (Redux, Zustand, Jotai) for application-wide state
- Keep state as local as possible
- Separate UI state from application state
- Use appropriate memoization (useMemo, useCallback) to optimize renders

## Hooks
- Follow the Rules of Hooks
- Use custom hooks to share logic between components
- Name hooks with "use" prefix
- Place hooks at the top level of your component
- Use useEffect for side effects with proper cleanup
- Use dependency arrays correctly in useEffect, useMemo, and useCallback

## Styling
- Choose a consistent approach: CSS Modules, Styled Components, Tailwind, etc.
- Keep styles close to the components they apply to
- Use responsive design principles
- Implement proper theming support
- Consider accessibility in your styling choices
- Extract common styles into reusable components or variables

## Performance
- Use React.memo for pure components that render often
- Use virtualization for long lists (react-window, react-virtualized)
- Avoid unnecessary rerenders by proper use of memoization
- Lazy load components and routes when appropriate
- Implement code-splitting for larger applications
- Avoid inline object/array creation in render functions

## Best Practices
- Use keys properly in lists
- Use fragments to avoid unnecessary DOM nodes
- Handle errors gracefully with Error Boundaries
- Keep side effects out of the render phase
- Use portals for modals and overlays
- Implement proper form handling (controlled components or libraries)
- Follow accessibility guidelines (semantic HTML, ARIA attributes)

## Testing
- Write unit tests for components using React Testing Library
- Test behavior rather than implementation details
- Mock external dependencies
- Test user interactions
- Implement integration tests for critical flows
