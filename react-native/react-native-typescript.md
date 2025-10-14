# React Native with TypeScript - AI Coding Rules

## General Code Style & Formatting
- Use functional and declarative programming patterns; avoid classes unless absolutely necessary
- Prefer iteration and modularization over code duplication
- Use descriptive variable names with auxiliary verbs (e.g., `isLoading`, `hasError`, `canSubmit`)
- Structure files in this order: exported component, subcomponents, helpers, static content, types
- Follow Expo's official documentation for setting up and configuring projects
- Keep components under 200 lines; extract larger components into smaller, focused ones

## Naming Conventions
- Use lowercase with dashes for directories (e.g., `components/auth-wizard`, `screens/user-profile`)
- Use PascalCase for component names and interfaces
- Use camelCase for variables, functions, and props
- Use SCREAMING_SNAKE_CASE for constants
- Favor named exports for components over default exports
- Use descriptive names that explain intent, not implementation

## TypeScript Best Practices
- Use TypeScript for all code; prefer interfaces over types for object shapes
- Avoid `any` and `enums`; use explicit types and const assertions instead
- Use functional components with TypeScript interfaces for props
- Enable strict mode in TypeScript configuration for better type safety
- Define proper return types for functions, especially async functions
- Use generic types for reusable components and utilities
- Leverage union types for component variants and state management

## Syntax & Formatting
- Use the `function` keyword for pure functions and arrow functions for callbacks
- Avoid unnecessary curly braces in conditionals; use concise syntax for simple statements
- Use declarative JSX with proper indentation
- Use Prettier for consistent code formatting with 2-space indentation
- Prefer template literals over string concatenation
- Use optional chaining (`?.`) and nullish coalescing (`??`) operators

## Styling & UI
- Use Expo's built-in components for common UI patterns and layouts
- Implement responsive design with Flexbox and `useWindowDimensions` hook
- Use `styled-components` or StyleSheet for styling; avoid inline styles
- Implement dark mode support using Expo's `useColorScheme` hook
- Ensure high accessibility (a11y) standards using ARIA roles and native accessibility props
- Use `react-native-reanimated` and `react-native-gesture-handler` for performant animations
- Follow platform-specific design guidelines (Material Design for Android, Human Interface Guidelines for iOS)

## State Management
- Use React hooks (`useState`, `useEffect`, `useContext`) for local state
- Implement Context API for global state when needed
- Consider Redux Toolkit for complex state management
- Use custom hooks to encapsulate stateful logic
- Avoid prop drilling; use context or state management libraries
- Keep state as close to where it's used as possible

## Performance Optimization
- Use `React.memo` for expensive components that receive stable props
- Implement `useMemo` and `useCallback` for expensive calculations and functions
- Use FlatList for large lists instead of ScrollView
- Optimize images with proper sizing and lazy loading
- Avoid creating objects and functions in render methods
- Use `getItemLayout` for FlatList when item heights are known

## Error Handling
- Implement proper error boundaries for component error handling
- Use try-catch blocks for async operations
- Provide meaningful error messages to users
- Log errors appropriately for debugging
- Handle network errors gracefully with retry mechanisms
- Validate user input and provide immediate feedback

## Testing
- Write unit tests for utility functions and custom hooks
- Use React Native Testing Library for component testing
- Implement integration tests for critical user flows
- Mock external dependencies and APIs in tests
- Aim for at least 80% code coverage on critical paths
- Test both success and error scenarios

