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

### Example: Proper TypeScript Usage

```tsx
// ✅ Good: Proper interfaces and types
interface User {
  id: string;
  name: string;
  email: string;
  age: number;
}

interface UserCardProps {
  user: User;
  onPress: (userId: string) => void;
  variant?: 'default' | 'compact';
}

type LoadingState = 'idle' | 'loading' | 'success' | 'error';

const UserCard: React.FC<UserCardProps> = ({ user, onPress, variant = 'default' }) => {
  const handlePress = (): void => {
    onPress(user.id);
  };

  return (
    <TouchableOpacity onPress={handlePress}>
      <Text>{user.name}</Text>
      {variant === 'default' && <Text>{user.email}</Text>}
    </TouchableOpacity>
  );
};

// ❌ Bad: Using any and poor typing
const UserCard = ({ user, onPress, variant }: any) => {
  const handlePress = () => {
    onPress(user.id);
  };

  return (
    <TouchableOpacity onPress={handlePress}>
      <Text>{user.name}</Text>
      {variant === 'default' && <Text>{user.email}</Text>}
    </TouchableOpacity>
  );
};
```

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

### Example: Custom Hook for State Management

```tsx
// ✅ Good: Custom hook with proper typing
interface UserState {
  users: User[];
  loading: boolean;
  error: string | null;
}

interface UseUsersReturn {
  users: User[];
  loading: boolean;
  error: string | null;
  fetchUsers: () => Promise<void>;
  addUser: (user: Omit<User, 'id'>) => Promise<void>;
}

const useUsers = (): UseUsersReturn => {
  const [state, setState] = useState<UserState>({
    users: [],
    loading: false,
    error: null,
  });

  const fetchUsers = useCallback(async (): Promise<void> => {
    setState(prev => ({ ...prev, loading: true, error: null }));
    try {
      const users = await userService.getUsers();
      setState(prev => ({ ...prev, users, loading: false }));
    } catch (error) {
      setState(prev => ({ 
        ...prev, 
        error: error instanceof Error ? error.message : 'Unknown error',
        loading: false 
      }));
    }
  }, []);

  const addUser = useCallback(async (userData: Omit<User, 'id'>): Promise<void> => {
    try {
      const newUser = await userService.createUser(userData);
      setState(prev => ({ 
        ...prev, 
        users: [...prev.users, newUser] 
      }));
    } catch (error) {
      setState(prev => ({ 
        ...prev, 
        error: error instanceof Error ? error.message : 'Failed to add user'
      }));
    }
  }, []);

  return {
    users: state.users,
    loading: state.loading,
    error: state.error,
    fetchUsers,
    addUser,
  };
};
```

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


## Patterns You should follow: React Native + TypeScript

### 1) Typed Navigation Params (React Navigation)
```tsx
// ✅ Good
type RootStackParamList = {
  Home: undefined;
  Profile: { userId: string };
};

type ProfileProps = NativeStackScreenProps<RootStackParamList, 'Profile'>;

export function ProfileScreen({ route }: ProfileProps) {
  const { userId } = route.params; // typed
  return <Text>{userId}</Text>;
}

// ❌ Bad: any params
export function ProfileScreenAny({ route }: any) {
  return <Text>{route.params.userId}</Text>;
}
```

### 2) Future-proof Component Props with Discriminated Unions
```tsx
// ✅ Good
type ButtonVariant =
  | { kind: 'primary'; onPress: () => void }
  | { kind: 'link'; href: string };

interface AppButtonProps extends ButtonVariant { label: string }

export function AppButton(props: AppButtonProps) {
  if (props.kind === 'primary') return <Button title={props.label} onPress={props.onPress} />;
  return (
    <TouchableOpacity onPress={() => Linking.openURL(props.href)}>
      <Text>{props.label}</Text>
    </TouchableOpacity>
  );
}

// ❌ Bad: optional props without intent
export function BadButton({ label, onPress, href }: { label: string; onPress?: any; href?: any }) {
  return <Text onPress={onPress || (() => Linking.openURL(href))}>{label}</Text>;
}
```

### 3) Stable Callbacks to Avoid Re-renders
```tsx
// ✅ Good
const ItemRow = React.memo(({ item, onSelect }: { item: Item; onSelect: (id: string) => void }) => {
  const handleSelect = useCallback(() => onSelect(item.id), [item.id, onSelect]);
  return <Text onPress={handleSelect}>{item.name}</Text>;
});

// ❌ Bad
const BadItemRow = ({ item, onSelect }: any) => (
  <Text onPress={() => onSelect(item.id)}>{item.name}</Text>
);
```

### 4) FlatList Key Extractor and getItemLayout
```tsx
// ✅ Good
<FlatList
  data={items}
  renderItem={renderItem}
  keyExtractor={(it) => it.id}
  getItemLayout={(_, index) => ({ length: 64, offset: 64 * index, index })}
/>
```
```tsx
// ❌ Bad: unstable keys and no getItemLayout
<FlatList
  data={items}
  renderItem={renderItem}
  // using index leads to poor recycling and re-renders
  keyExtractor={(_, index) => String(index)}
/>
```

### 5) API Client with Narrowed Error Types
```ts
// ✅ Good
interface ApiError { status: number; message: string }

async function fetchJson<T>(url: string): Promise<T> {
  const res = await fetch(url);
  if (!res.ok) throw { status: res.status, message: await res.text() } as ApiError;
  return (await res.json()) as T;
}
```
```ts
// ❌ Bad: no status check, untyped response
async function fetchJsonBad(url: string) {
  const res = await fetch(url);
  return res.json();
}
```

### 6) Abortable Requests with useEffect Cleanup
```tsx
// ✅ Good
useEffect(() => {
  const controller = new AbortController();
  fetch(url, { signal: controller.signal });
  return () => controller.abort();
}, [url]);
```
```tsx
// ❌ Bad: no cleanup, leaks fetch on unmount
useEffect(() => {
  fetch(url);
}, [url]);
```

### 7) Theming with Context and Typed Tokens
```tsx
// ✅ Good
type Theme = { colors: { bg: string; text: string; accent: string } };
const ThemeContext = createContext<Theme | null>(null);
export const useTheme = () => {
  const theme = useContext(ThemeContext);
  if (!theme) throw new Error('ThemeProvider missing');
  return theme;
};
```
```tsx
// ❌ Bad: untyped context and unsafe access
const ThemeCtx = createContext<any>(null);
export const useThemeBad = () => useContext(ThemeCtx).colors.accent;
```

### 8) Accessible Touch Targets
```tsx
// ✅ Good
<TouchableOpacity accessibilityRole="button" accessibilityLabel="Add to cart" hitSlop={8}>
  <Text>Add</Text>
</TouchableOpacity>
```
```tsx
// ❌ Bad: tiny touch target, no a11y label
<TouchableOpacity>
  <Text>Add</Text>
</TouchableOpacity>
```

### 9) Image Caching with FastImage
```tsx
// ✅ Good
<FastImage
  style={{ width: 120, height: 120 }}
  source={{ uri, priority: FastImage.priority.high, cache: FastImage.cacheControl.immutable }}
  resizeMode={FastImage.resizeMode.cover}
/>
```
```tsx
// ❌ Bad: default Image without caching or sizing discipline
<Image source={{ uri }} />
```

### 10) Reanimated Layout Animations (JSI)
```tsx
// ✅ Good (worklet-safe)
const entering = FadeIn.duration(150);
const exiting = FadeOut.duration(150);
return <Animated.View entering={entering} exiting={exiting}><Text>Hi</Text></Animated.View>;
```
```tsx
// ❌ Bad: JS-driven animation without native driver
Animated.timing(opacity, { toValue: 1, duration: 300, useNativeDriver: false }).start();
```

### 11) Debounced Search Hook
```ts
// ✅ Good
export function useDebounce(value: string, delayMs = 300) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const t = setTimeout(() => setDebounced(value), delayMs);
    return () => clearTimeout(t);
  }, [value, delayMs]);
  return debounced;
}
```
```tsx
// ❌ Bad: fires request on every keystroke
const [q, setQ] = useState('');
useEffect(() => { search(q); }, [q]);
```

### 12) Infinite Scroll with Guard Clauses
```tsx
// ✅ Good
const onEndReached = () => {
  if (isLoading || !hasMore) return;
  loadMore();
};
```
```tsx
// ❌ Bad: triggers while loading, duplicates requests
const onEndReachedBad = () => { loadMore(); };
```

### 13) Error Boundary
```tsx
// ✅ Good
class ErrorBoundary extends React.Component<{ children: React.ReactNode }, { hasError: boolean }> {
  state = { hasError: false };
  static getDerivedStateFromError() { return { hasError: true }; }
  componentDidCatch(err: unknown) { /* log */ }
  render() { return this.state.hasError ? <Text>Something went wrong</Text> : this.props.children; }
}
```
```tsx
// ❌ Bad: no error boundary; errors crash the app tree
// (nothing wraps the root navigator)
```

### 14) Zod Schemas for Runtime Validation
```ts
// ✅ Good
const UserSchema = z.object({ id: z.string(), name: z.string(), email: z.string().email() });
type User = z.infer<typeof UserSchema>;
```
```ts
// ❌ Bad: trust incoming JSON without validation
type UserBad = { id: string; name: string; email: string };
const user: UserBad = await fetchJson('/user');
```

### 15) Secure Storage Wrapper
```ts
// ✅ Good
export const secureStorage = {
  async get(key: string) { return await SecureStore.getItemAsync(key); },
  async set(key: string, value: string) { await SecureStore.setItemAsync(key, value); },
  async remove(key: string) { await SecureStore.deleteItemAsync(key); },
};
```
```ts
// ❌ Bad: store secrets in AsyncStorage
await AsyncStorage.setItem('token', token);
```

### 16) Controlled TextInput with Keyboard Handling
```tsx
// ✅ Good
const [value, setValue] = useState('');
return (
  <KeyboardAvoidingView behavior={Platform.OS === 'ios' ? 'padding' : undefined}>
    <TextInput value={value} onChangeText={setValue} autoCapitalize="none" />
  </KeyboardAvoidingView>
);
```
```tsx
// ❌ Bad: uncontrolled, keyboard obscures input
<TextInput />
```

### 17) Memoized Selectors in Context
```tsx
// ✅ Good
const UsersContext = createContext<User[] | null>(null);
export function useUserById(id: string) {
  const users = useContext(UsersContext) ?? [];
  return useMemo(() => users.find(u => u.id === id) ?? null, [users, id]);
}
```
```tsx
// ❌ Bad: recomputes every render
export function useUserByIdBad(id: string) {
  const users = useContext(UsersContext) ?? [];
  return users.find(u => u.id === id) ?? null;
}
```

### 18) Platform-specific Code Splits
```tsx
// ✅ Good
const DatePicker = Platform.select({ ios: IOSDatePicker, android: AndroidDatePicker })!;
```
```tsx
// ❌ Bad: heavy runtime branching inline
const DatePickerBad = (props: any) => Platform.OS === 'ios' ? <IOSDatePicker {...props} /> : <AndroidDatePicker {...props} />;
```

### 19) Background Task Registration (Expo)
```ts
// ✅ Good
TaskManager.defineTask('sync-task', async () => { /* sync */ });
await BackgroundFetch.registerTaskAsync('sync-task', { minimumInterval: 900 });
```
```ts
// ❌ Bad: register in component render (runs repeatedly)
BackgroundFetch.registerTaskAsync('sync-task');
```

### 20) i18n with Typed Keys
```ts
// ✅ Good
const messages = { home_title: 'Home', profile_title: 'Profile' } as const;
type MessageKey = keyof typeof messages;
export function t(key: MessageKey) { return messages[key]; }
```
```ts
// ❌ Bad: hardcoded strings sprinkled across components
<Text>Profile</Text>
```

