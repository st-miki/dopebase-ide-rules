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


## Patterns You should follow: Flutter + Dart

### 1) Stateless vs Stateful Split
```dart
// ✅ Good: Stateless for pure UI
class PriceTag extends StatelessWidget {
  final double price;
  const PriceTag({super.key, required this.price});
  @override
  Widget build(BuildContext context) => Text('\$${price.toStringAsFixed(2)}');
}

// ✅ Stateful only when needed
class Counter extends StatefulWidget { const Counter({super.key}); @override State<Counter> createState() => _CounterState(); }
class _CounterState extends State<Counter> { int count = 0; @override Widget build(BuildContext c) => ElevatedButton(onPressed: () => setState(()=>count++), child: Text('$count')); }
```
```dart
// ❌ Bad: Unnecessary StatefulWidget and string concatenation
class PriceTagBad extends StatefulWidget { final double price; const PriceTagBad({super.key, required this.price}); @override State<PriceTagBad> createState() => _PriceTagBadState(); }
class _PriceTagBadState extends State<PriceTagBad> { @override Widget build(BuildContext context) => Text('\$' + widget.price.toString()); }
```

### 2) const Constructors to Reduce Rebuilds
```dart
// ✅ Good
const SizedBox spacer = SizedBox(height: 16);
```
```dart
// ❌ Bad: non-const leads to rebuilds
final spacerBad = SizedBox(height: 16);
```

### 3) ListView.builder for Large Lists
```dart
// ✅ Good
ListView.builder(
  itemCount: items.length,
  itemBuilder: (_, i) => ListTile(title: Text(items[i].title)),
)
```
```dart
// ❌ Bad: ListView with many children
ListView(children: items.map((e) => ListTile(title: Text(e.title))).toList())
```

### 4) Selector with Provider to Minimize Rebuilds
```dart
// ✅ Good
Selector<UserStore, String>(
  selector: (_, store) => store.currentUser.name,
  builder: (_, name, __) => Text(name),
)
```
```dart
// ❌ Bad: Consumer rebuilds entire subtree unnecessarily
Consumer<UserStore>(builder: (_, store, __) => Text(store.currentUser.name))
```

### 5) Riverpod Typed Providers
```dart
// ✅ Good
final userRepoProvider = Provider<UserRepository>((ref) => UserRepository());
final userFutureProvider = FutureProvider.autoDispose<List<User>>((ref) async {
  final repo = ref.read(userRepoProvider);
  return repo.fetchUsers();
});
```
```dart
// ❌ Bad: global singletons and manual caching
late final userRepo = UserRepository();
Future<List<User>> getUsers() => userRepo.fetchUsers();
```

### 6) Bloc Events and States with freezed
```dart
// ✅ Good
@freezed
class LoginEvent with _$LoginEvent { const factory LoginEvent.submitted(String email, String password) = _Submitted; }
@freezed
class LoginState with _$LoginState { const factory LoginState.idle() = _Idle; const factory LoginState.loading() = _Loading; const factory LoginState.success(User u) = _Success; const factory LoginState.error(String msg) = _Error; }
```
```dart
// ❌ Bad: stringly-typed states
class LoginStateBad { final String state; LoginStateBad(this.state); }
```

### 7) JSON Serialization via json_serializable
```dart
// ✅ Good
@JsonSerializable()
class User { final String id; final String name; User({required this.id, required this.name}); factory User.fromJson(Map<String, dynamic> j) => _$UserFromJson(j); Map<String, dynamic> toJson() => _$UserToJson(this); }
```
```dart
// ❌ Bad: manual parsing without null checks
class UserBad { UserBad.fromJson(Map<String, dynamic> j) { /* direct casts */ } }
```

### 8) Dio Client with Interceptors
```dart
// ✅ Good
final dio = Dio(BaseOptions(connectTimeout: const Duration(seconds: 10)));
dio.interceptors.add(InterceptorsWrapper(onRequest: (o, h) { o.headers['X-App'] = 'myapp'; return h.next(o); }));
```
```dart
// ❌ Bad: raw HttpClient everywhere without timeouts
final client = HttpClient();
```

### 9) Error Handling: Catch Exceptions, Preserve Stack
```dart
// ✅ Good
try { await repo.fetch(); } on TimeoutException catch (e, st) { log('Timeout', error: e, stackTrace: st); rethrow; } on DioError catch (e, st) { log('HTTP', error: e, stackTrace: st); }
```
```dart
// ❌ Bad: catch-all and swallow
try { await repo.fetch(); } catch (_) {}
```

### 10) RepaintBoundary for Expensive Widgets
```dart
// ✅ Good
const RepaintBoundary(child: ComplexChart())
```
```dart
// ❌ Bad: no boundary; parent rebuild repaints heavy child
ComplexChart()
```

### 11) Debounced Search with RxDart
```dart
// ✅ Good
final queryController = BehaviorSubject<String>();
late final Stream<List<User>> results = queryController
  .debounceTime(const Duration(milliseconds: 300))
  .switchMap((q) => Stream.fromFuture(api.search(q)));
```
```dart
// ❌ Bad: call API on every keypress without debounce
onChanged: (q) => api.search(q)
```

### 12) Pagination Guard Clauses
```dart
// ✅ Good
void onLoadMore() {
  if (state.isLoading || !state.hasMore) return;
  context.read<ListCubit>().loadMore();
}
```
```dart
// ❌ Bad: triggers multiple overlapping loads
void onLoadMoreBad() { context.read<ListCubit>().loadMore(); }
```

### 13) Isolate for CPU-heavy Work
```dart
// ✅ Good
final parsed = await compute(parseLargeJson, jsonString);
```
```dart
// ❌ Bad: parse on UI thread
final parsed = parseLargeJson(jsonString);
```

### 14) CachedNetworkImage
```dart
// ✅ Good
CachedNetworkImage(imageUrl: url, placeholder: (_, __) => const CircularProgressIndicator());
```
```dart
// ❌ Bad: Image.network without caching or placeholder
Image.network(url)
```

### 15) Navigator 2.0 Typed Routes (go_router)
```dart
// ✅ Good
final _router = GoRouter(routes: [ GoRoute(path: '/', builder: (_, __) => const Home()), GoRoute(path: '/user/:id', builder: (_, st) => UserPage(id: st.pathParameters['id']!)), ]);
```
```dart
// ❌ Bad: push with string concatenation
Navigator.of(context).pushNamed('/user/' + id);
```

### 16) Theme Extensions for Design Tokens
```dart
// ✅ Good
@immutable
class AppTokens extends ThemeExtension<AppTokens> { const AppTokens({required this.accent}); final Color accent; @override AppTokens copyWith({Color? accent}) => AppTokens(accent: accent ?? this.accent); @override AppTokens lerp(ThemeExtension<AppTokens>? other, double t) => this; }
```
```dart
// ❌ Bad: magic numbers/colors scattered
const Color kAccent = Color(0xFF2196F3);
```

### 17) Accessibility with Semantics
```dart
// ✅ Good
Semantics(button: true, label: 'Add to cart', child: ElevatedButton(onPressed: add, child: const Text('Add')))
```
```dart
// ❌ Bad: missing semantics label
ElevatedButton(onPressed: add, child: const Text('Add'))
```

### 18) Implicit Animations
```dart
// ✅ Good
AnimatedContainer(duration: const Duration(milliseconds: 200), width: expanded ? 200 : 100)
```
```dart
// ❌ Bad: abrupt change without animation
Container(width: expanded ? 200 : 100)
```

### 19) Background Tasks (workmanager)
```dart
// ✅ Good
Workmanager().initialize(callbackDispatcher);
Workmanager().registerPeriodicTask('sync', 'syncTask', frequency: const Duration(minutes: 15));
```
```dart
// ❌ Bad: register in build()
@override Widget build(BuildContext c) { Workmanager().registerPeriodicTask('sync', 'syncTask'); return const SizedBox(); }
```

### 20) Platform Channels
```dart
// ✅ Good
const platform = MethodChannel('com.example/native');
final version = await platform.invokeMethod<String>('getVersion');
```
```dart
// ❌ Bad: missing type and error handling
final version = await const MethodChannel('com.example/native').invokeMethod('getVersion');
```