# iOS SwiftUI - AI Coding Rules

## General Code Style & Formatting
- Follow Swift's official API Design Guidelines for consistent code style
- Use meaningful and descriptive names for variables, functions, and types
- Prefer composition over inheritance when building UI components
- Keep functions and methods focused on a single responsibility
- Use proper indentation and consistent formatting throughout the codebase
- Follow Swift naming conventions: camelCase for variables, PascalCase for types

## SwiftUI Best Practices
- Use `@State` for local view state that changes over time
- Use `@Binding` to create two-way connections between views
- Use `@ObservedObject` for external objects that conform to `ObservableObject`
- Use `@StateObject` for creating and owning observable objects
- Use `@EnvironmentObject` for shared data across the view hierarchy
- Prefer declarative syntax over imperative programming patterns

## View Architecture
- Keep views small and focused on a single responsibility
- Extract complex views into smaller, reusable components
- Use proper view modifiers to compose functionality
- Implement proper view lifecycle management
- Use `ViewBuilder` for conditional view rendering
- Avoid deep nesting by extracting subviews

## Data Flow
- Use `ObservableObject` for data that needs to be shared across views
- Implement proper data binding with `@Binding` and `@Published`
- Use `@State` for view-specific state that doesn't need to be shared
- Implement proper data validation and error handling
- Use `Combine` framework for reactive programming patterns
- Handle data loading states appropriately

## Performance Optimization
- Use `LazyVStack` and `LazyHStack` for large lists
- Implement proper view identity with `id()` modifier
- Use `@State` and `@StateObject` appropriately to avoid unnecessary updates
- Avoid creating objects in view body
- Use `onAppear` and `onDisappear` for lifecycle management
- Profile performance using Instruments

## Navigation
- Use `NavigationView` and `NavigationLink` for hierarchical navigation
- Implement proper navigation state management
- Use `@State` for navigation-related state
- Handle deep linking and navigation restoration
- Use `sheet` and `fullScreenCover` for modal presentations
- Implement proper back navigation handling

## Accessibility
- Use semantic modifiers like `accessibilityLabel` and `accessibilityHint`
- Implement proper accessibility navigation
- Use `accessibilityAddTraits` for interactive elements
- Test with VoiceOver and other accessibility tools
- Provide alternative text for images and icons
- Ensure proper contrast ratios for text and backgrounds

## Error Handling
- Use `Result` type for operations that can fail
- Implement proper error states in your views
- Use `Alert` and `ActionSheet` for user error notifications
- Handle network errors gracefully
- Implement retry mechanisms for failed operations
- Log errors appropriately for debugging

## Testing
- Write unit tests for business logic and data models
- Use `ViewInspector` for SwiftUI view testing
- Implement UI tests for critical user flows
- Mock external dependencies in tests
- Test error scenarios and edge cases
- Use `XCTest` framework for comprehensive testing

## Platform Integration
- Use `UIKit` integration when SwiftUI doesn't provide needed functionality
- Implement proper platform-specific adaptations
- Use `UIViewRepresentable` for UIKit component integration
- Handle platform differences gracefully
- Use native iOS design patterns and conventions
- Test on different iOS versions and device sizes

## Code Organization
- Organize files by feature, not by file type
- Use proper import statements and avoid circular dependencies
- Implement proper separation of concerns
- Use extensions to organize related functionality
- Create reusable components and utilities
- Follow consistent naming conventions across the project

## Memory Management
- Use weak references to avoid retain cycles
- Implement proper cleanup in view lifecycle methods
- Use `@StateObject` and `@ObservedObject` appropriately
- Avoid strong reference cycles in closures
- Monitor memory usage in development and production
- Use proper disposal patterns for resources

