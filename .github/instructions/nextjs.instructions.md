---
applyTo: "**/*.jsx,**/*.tsx,**/*next*/**"
---
# Next.js Style Guide

## Project Structure
- Follow the standard Next.js directory structure (pages, public, styles)
- Use the app directory for newer projects leveraging the App Router
- Organize pages by feature or route structure
- Place reusable components in a components directory
- Use a lib or utils directory for helper functions
- Store API routes in the api directory
- Keep configuration files at the root level

## Routing
- Use the file-system based routing approach
- Implement dynamic routes with appropriate naming ([id].js)
- Use shallow routing when applicable
- Implement proper error pages (404, 500)
- Add proper metadata for SEO using Next.js metadata API
- Use Link component for client-side navigation between pages
- Implement proper handling of query parameters

## Data Fetching
- Choose appropriate data fetching method based on requirements:
  - getStaticProps for static data
  - getServerSideProps for dynamic server-rendered data
  - getStaticPaths for dynamic routes with static generation
  - SWR or React Query for client-side data fetching with caching
- Implement proper error handling for data fetching operations
- Use Incremental Static Regeneration (ISR) for data that changes occasionally
- Cache API responses appropriately

## Performance
- Use Image component for optimized images
- Implement proper code splitting with dynamic imports
- Utilize Next.js built-in performance optimizations
- Implement proper caching strategies (Cache-Control headers)
- Use Server Components when appropriate (App Router)
- Optimize third-party script loading with next/script
- Implement prefetching for anticipated user navigation

## State Management
- Use local state for component-specific state
- Consider using Context API for shared state across components
- Use external state management libraries (Redux, Zustand) for complex applications
- Implement proper data persistence when needed (localStorage, cookies)
- Use React Query or SWR for server state

## API Routes
- Implement proper validation for API inputs
- Use appropriate HTTP methods (GET, POST, PUT, DELETE)
- Return consistent response formats
- Implement proper error handling and status codes
- Secure routes with authentication when needed
- Consider rate limiting for public APIs

## Authentication
- Use NextAuth.js or a similar solution for authentication
- Secure API routes with proper middleware
- Implement proper role-based access control
- Use secure cookies or JWT for session management
- Handle authentication state properly on the client side

## Deployment & Environment
- Use environment variables for configuration
- Keep sensitive information out of client-side code
- Consider using Vercel or similar platforms for deployment
- Implement proper CI/CD pipeline
- Use feature flags for controlled feature rollout

## Testing
- Write unit tests for components and utility functions
- Implement integration tests for critical user flows
- Use Cypress or Playwright for end-to-end testing
- Mock API responses in tests
- Test different rendering strategies (SSR, SSG, CSR)
