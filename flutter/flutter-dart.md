# Flutter with Dart - AI Coding Rules

## General Code Style & Formatting
- Use the `const` keyword whenever possible to optimize performance and reduce memory usage
- Follow the official Dart style guide for consistent code formatting
- Use meaningful variable and function names that clearly express intent
- Keep functions short and single-purpose (ideally under 20 lines)
- Avoid deeply nested code; use early returns and extract logic into utility functions
- Use proper indentation (2 spaces) and consistent formatting throughout the codebase

## Naming Conventions
- Use PascalCase for class names, enums, and typedefs
- Use camelCase for variable names, function names, and method names
- Use lowercase_with_underscores for file names and directory names
- Use SCREAMING_SNAKE_CASE for constants and enum values
- Use descriptive names that explain what the code does, not how it does it
- Avoid abbreviations unless they are widely understood

## Widget Architecture
- Keep widgets small and focused on a single responsibility
- Use composition over inheritance when building complex UIs
- Extract reusable widgets into separate files
- Use `StatelessWidget` for widgets that don't need to maintain state
- Use `StatefulWidget` only when necessary for state management
- Implement proper widget lifecycle management

## State Management
- Use `ChangeNotifier` and `Provider` for simple state management
- Consider `Bloc` or `Riverpod` for complex applications
- Keep state as close to where it's used as possible
- Use immutable data models to ensure data integrity
- Implement proper state updates to avoid unnecessary rebuilds
- Use `setState` sparingly and only for local widget state

## Performance Optimization
- Prefer traditional `for` loops over `forEach` for better performance
- Use `const` constructors to reduce widget rebuilds
- Implement proper list building with `ListView.builder` for large datasets
- Use `RepaintBoundary` to isolate expensive widgets
- Avoid creating widgets in build methods
- Use `FutureBuilder` and `StreamBuilder` efficiently

## Error Handling
- Do not catch `Errors` (e.g., `StateError` or `OutOfMemoryError`)
- Focus on catching `Exceptions` which are designed to be caught
- Use exceptions for error handling and preserve stack traces
- Avoid ignoring exceptions; always handle or rethrow them
- Create specialized exception classes for better error handling
- Implement proper error boundaries and user feedback

## Data Handling
- Use immutable data models with `final` properties
- Implement proper serialization and deserialization
- Use `json_annotation` for automatic JSON handling
- Validate data at the boundaries of your application
- Use proper data types and avoid dynamic when possible
- Implement proper null safety throughout the codebase

## Testing
- Write unit tests for business logic and utility functions
- Use widget tests for UI component testing
- Implement integration tests for critical user flows
- Mock external dependencies and services
- Aim for high test coverage on critical paths
- Use `flutter_test` package for comprehensive testing

## File Organization
- Organize files by feature, not by file type
- Use barrel exports (index.dart) for clean imports
- Keep related files in the same directory
- Use consistent naming conventions across the project
- Separate business logic from UI code
- Use proper package structure for larger applications

## Accessibility
- Implement proper semantic labels for screen readers
- Use appropriate contrast ratios for text and backgrounds
- Provide alternative text for images and icons
- Ensure proper focus management for keyboard navigation
- Test with accessibility tools and real users
- Follow WCAG guidelines for web accessibility

## Platform Integration
- Use platform-specific code when necessary
- Implement proper platform channels for native functionality
- Handle platform differences gracefully
- Use platform-specific widgets when appropriate
- Test on both iOS and Android devices
- Follow platform-specific design guidelines

