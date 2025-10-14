# React with TypeScript - Web Development Rules

## General Code Style & Formatting
- Use functional components with hooks instead of class components
- Prefer composition over inheritance for component design
- Use descriptive variable names with clear intent (e.g., `isLoading`, `hasError`)
- Structure files: exports, components, hooks, utilities, types, constants
- Follow consistent indentation (2 spaces) and formatting with Prettier
- Keep components under 200 lines; extract larger components into smaller ones

## TypeScript Best Practices
- Use TypeScript for all code; prefer interfaces over types for object shapes
- Avoid `any` type; use explicit types or `unknown` when necessary
- Use generic types for reusable components and utilities
- Enable strict mode in TypeScript configuration
- Define proper return types for functions, especially async functions
- Use union types for component variants and state management
- Leverage TypeScript's utility types (Pick, Omit, Partial, etc.)

## Component Architecture
- Use functional components with hooks for state management
- Implement proper component composition and reusability
- Use custom hooks to encapsulate stateful logic
- Keep components focused on a single responsibility
- Use proper prop types and default values
- Implement proper component lifecycle management

## State Management
- Use `useState` for local component state
- Use `useContext` for sharing state across components
- Consider Redux Toolkit for complex global state management
- Use `useReducer` for complex state logic
- Implement proper state updates and immutability
- Use custom hooks for stateful logic reuse

## Performance Optimization
- Use `React.memo` for components that receive stable props
- Implement `useMemo` for expensive calculations
- Use `useCallback` for functions passed as props
- Use `React.lazy` and `Suspense` for code splitting
- Implement proper list virtualization for large datasets
- Avoid creating objects and functions in render methods

## Styling & UI
- Use CSS Modules, styled-components, or Tailwind CSS for styling
- Implement responsive design with CSS Grid and Flexbox
- Use CSS custom properties for theming and consistency
- Implement dark mode support with CSS variables
- Ensure high accessibility standards with proper ARIA attributes
- Use semantic HTML elements for better accessibility

## Error Handling
- Implement error boundaries for component error handling
- Use try-catch blocks for async operations
- Provide meaningful error messages to users
- Log errors appropriately for debugging
- Handle network errors gracefully with retry mechanisms
- Implement proper loading and error states

## Testing
- Write unit tests for components and utilities
- Use React Testing Library for component testing
- Implement integration tests for critical user flows
- Mock external dependencies and APIs in tests
- Aim for high test coverage on critical paths
- Test both success and error scenarios

## Routing & Navigation
- Use React Router for client-side routing
- Implement proper route protection and authentication
- Use lazy loading for route-based code splitting
- Handle browser history and navigation properly
- Implement proper 404 and error page handling
- Use proper route parameters and query strings

## API Integration
- Use fetch API or axios for HTTP requests
- Implement proper error handling for API calls
- Use React Query or SWR for data fetching and caching
- Implement proper loading states for async operations
- Handle network connectivity and offline scenarios
- Use proper request/response interceptors

## Build & Deployment
- Use Create React App or Vite for project setup
- Implement proper environment variable management
- Use proper build optimization and code splitting
- Implement proper asset optimization and compression
- Use proper deployment strategies and CI/CD
- Monitor performance and errors in production

