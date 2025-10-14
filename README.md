# Dopebase IDE Rules

A comprehensive collection of AI-powered coding rules and best practices for modern development environments. This repository contains curated rules for various technologies and frameworks to help you get the best results from AI coding assistants.

## What's Included

This repository contains **15+ rule files** organized by technology:

### Mobile Development
- **React Native** - TypeScript best practices, performance optimization
- **Flutter** - Dart coding standards, state management patterns
- **iOS** - SwiftUI guidelines, iOS development best practices

### Web Development
- **React** - TypeScript integration, modern React patterns
- **Next.js** - Full-stack React framework best practices

### Backend & Systems
- **Python** - General best practices, web development, data science

## How to Use These Rules

### For Cursor IDE

Cursor is an AI-powered code editor that can use these rules to provide better suggestions and code generation.

#### Step 1: Create Rules Directory
In your project root, create a `.cursorrules` directory:

```bash
mkdir .cursorrules
```

#### Step 2: Copy Relevant Rules
Copy the rule files you need into the `.cursorrules` directory:

```bash
# For React Native projects
cp react-native/react-native-typescript.md .cursorrules/
cp react-native/performance-optimization.md .cursorrules/

# For Flutter projects
cp flutter/flutter-dart.md .cursorrules/
cp flutter/state-management.md .cursorrules/

# For web projects
cp web/react-typescript.md .cursorrules/
cp web/nextjs-best-practices.md .cursorrules/
```

#### Step 3: Reference Rules in Your Code
Use the `@filename` syntax to reference specific rules:

```javascript
// @react-native-typescript
// @performance-optimization
function MyComponent() {
  // Your code here - Cursor will follow the rules
}
```

#### Step 4: Use in Chat
When chatting with Cursor's AI, reference the rules:

```
@react-native-typescript Help me create a new component that follows these best practices
```

### For Windsurf

Make Windsurf use the exact rule files from this repo.

#### Option A: Reuse `.cursorrules` (recommended)
1. Keep using the `.cursorrules` folder from the Cursor steps above
2. Copy the relevant rule files into `.cursorrules/` (React Native, Flutter, Web, etc.)
3. In Windsurf, open the Rules/Context panel, click Add and select the `.cursorrules/` folder to index it
4. Pin the most important rule files so they are always included

Usage in chat/code:

```
# In chat
Include: .cursorrules/
Follow: react-native-typescript.md and performance-optimization.md

# In code comments to steer generations
// @react-native-typescript
// @performance-optimization
```

#### Option B: Use a `rules/` folder
1. Create `rules/` in your project root
2. Copy the rule files you want into `rules/`
3. In Windsurf, add `rules/` to the Rules/Context panel and pin key files
4. Reference them in prompts (e.g., “Use `rules/react-typescript.md` for patterns”)

### For Visual Studio Code

Make VS Code AI features (e.g., Copilot Chat, Codeium Chat) use the rule files directly.

#### Step 1: Put rules in your workspace
Pick one of the following:
- Keep using `.cursorrules/` from the Cursor steps
- Or create a `rules/` folder and copy the needed files there

#### Step 2: Install AI chat extension(s)
Install at least one chat extension so you can attach files/folders as context:

```bash
# For React/TypeScript
code --install-extension ms-vscode.vscode-typescript-next
code --install-extension bradlc.vscode-tailwindcss
code --install-extension esbenp.prettier-vscode

# For Python
code --install-extension ms-python.python
code --install-extension ms-python.flake8

```

#### Step 3: Configure VS Code behavior (optional but helpful)
Add baseline formatting/linting to `.vscode/settings.json`:

```json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.organizeImports": true
  },
  "typescript.preferences.importModuleSpecifier": "relative",
  "python.linting.enabled": true,
  "python.linting.flake8Enabled": true
}
```

#### Step 4: Tell the AI to use your rule files
With Copilot Chat or similar, include your rules as explicit context:

```
# Attach the whole folder
#folder .cursorrules
# or
#folder rules

# Attach specific files
#file .cursorrules/react-native-typescript.md
#file rules/nextjs-best-practices.md

# Example prompt
Use the attached rules. Build a new React component that follows `react-typescript.md` and `performance-optimization.md`.
```

In code, you can also steer completions by referencing rules in comments:

```ts
// @react-typescript
// @performance-optimization
export function MyComponent() {
  return null;
}
```

### For Other IDEs

#### JetBrains IDEs (IntelliJ, WebStorm, PyCharm, etc.)
1. Create a `rules` directory in your project
2. Copy relevant rule files
3. Reference them in TODO comments or documentation
4. Use them as guidelines when using AI assistants

#### Sublime Text, Vim, Emacs
1. Keep rule files in your project directory
2. Reference them when using AI plugins or external tools
3. Use them as coding standards documentation

## 🚀 Quick Start Examples

### React Native Project Setup
```bash
# 1. Create project
npx create-expo-app MyApp --template typescript

# 2. Add rules
mkdir .cursorrules
cp react-native/react-native-typescript.md .cursorrules/
cp react-native/performance-optimization.md .cursorrules/

# 3. Start coding with AI assistance
# Reference rules in your code comments
```

### Flutter Project Setup
```bash
# 1. Create project
flutter create my_app

# 2. Add rules
mkdir .cursorrules
cp flutter/flutter-dart.md .cursorrules/
cp flutter/state-management.md .cursorrules/

# 3. Start coding with AI assistance
```

### Next.js Project Setup
```bash
# 1. Create project
npx create-next-app@latest my-app --typescript --tailwind --eslint

# 2. Add rules
mkdir .cursorrules
cp web/react-typescript.md .cursorrules/
cp web/nextjs-best-practices.md .cursorrules/

# 3. Start coding with AI assistance
```

## Rule Categories

Each technology includes rules for:

- **Code Style & Formatting** - Consistent code appearance
- **Best Practices** - Language-specific recommendations
- **Performance** - Optimization techniques
- **Security** - Security best practices
- **Testing** - Testing strategies and patterns
- **Architecture** - Design patterns and structure
- **Error Handling** - Proper error management
- **Documentation** - Code documentation standards
=
## Resources

### Official Documentation
- [Cursor Documentation](https://cursor.sh/docs)
- [Windsurf Documentation](https://windsurf.com/docs)
- [VS Code AI Extensions](https://code.visualstudio.com/docs/editor/artificial-intelligence)

### Technology-Specific Resources
- [React Native Docs](https://reactnative.dev/docs/getting-started)
- [Flutter Docs](https://flutter.dev/docs)
- [Next.js Docs](https://nextjs.org/docs)
- [Python Best Practices](https://docs.python.org/3/tutorial/)
- [Go Best Practices](https://golang.org/doc/effective_go.html)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Happy Coding! **

Use these rules to get the best results from your AI coding assistants and build amazing software faster and more efficiently.
