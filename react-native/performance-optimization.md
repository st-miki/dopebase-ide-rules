# React Native Performance Optimization Rules

## Component Optimization
- Use `React.memo` for components that receive stable props and are expensive to render
- Implement `useMemo` for expensive calculations that depend on specific dependencies
- Use `useCallback` for functions passed as props to prevent unnecessary re-renders
- Avoid creating objects, arrays, or functions inside render methods
- Extract static values outside of components when possible
- Use `useRef` for values that don't need to trigger re-renders

## List Performance
- Always use `FlatList` instead of `ScrollView` for large datasets
- Implement `getItemLayout` when item heights are known and consistent
- Use `keyExtractor` prop for efficient list item identification
- Implement `removeClippedSubviews` for very long lists
- Use `initialNumToRender` and `maxToRenderPerBatch` for performance tuning
- Consider virtualization for extremely large datasets

## Image Optimization
- Use appropriate image formats (WebP for Android, HEIF for iOS when supported)
- Implement proper image sizing to avoid memory issues
- Use `resizeMode` appropriately for different use cases
- Implement lazy loading for images below the fold
- Cache images using libraries like `react-native-fast-image`
- Compress images before bundling them in the app

## Memory Management
- Clean up subscriptions in `useEffect` cleanup functions
- Remove event listeners when components unmount
- Use `WeakMap` and `WeakSet` for temporary object references
- Avoid memory leaks by properly disposing of timers and intervals
- Monitor memory usage in development and production builds
- Use `InteractionManager.runAfterInteractions` for non-critical operations

## Bundle Size Optimization
- Use dynamic imports for code splitting
- Remove unused dependencies and imports
- Use tree shaking to eliminate dead code
- Implement lazy loading for screens and components
- Optimize third-party library usage
- Use Metro bundler's built-in optimizations

## Network Performance
- Implement proper caching strategies for API calls
- Use request deduplication to avoid duplicate network calls
- Implement offline support with proper data synchronization
- Use compression for API responses when possible
- Implement retry mechanisms with exponential backoff
- Monitor network performance and optimize accordingly

## Animation Performance
- Use `react-native-reanimated` for complex animations
- Avoid using `Animated` API for performance-critical animations
- Use native driver when possible for better performance
- Implement proper animation cleanup
- Use `runOnJS` sparingly and only when necessary
- Optimize animation frame rates based on device capabilities

## Platform-Specific Optimizations
- Use platform-specific code when performance benefits are significant
- Implement native modules for CPU-intensive operations
- Use platform-specific image formats and optimizations
- Leverage platform-specific UI components when appropriate
- Test performance on both iOS and Android devices
- Use platform-specific debugging tools and profilers

