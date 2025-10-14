# Next.js - Best Practices & Rules

## Project Structure & Organization
- Use the `pages` directory for file-based routing
- Organize components in a `components` directory with proper categorization
- Use the `public` directory for static assets
- Implement proper folder structure: `components`, `pages`, `styles`, `utils`, `types`
- Use barrel exports (index.ts) for clean imports
- Follow consistent naming conventions across the project

## Routing & Navigation
- Use Next.js built-in routing with `useRouter` hook
- Implement proper dynamic routing with `[id].tsx` files
- Use `Link` component for client-side navigation
- Implement proper route protection and authentication
- Use `getStaticPaths` and `getStaticProps` for static generation
- Handle 404 pages and error boundaries properly

## Data Fetching
- Use `getStaticProps` for static data that doesn't change often
- Use `getServerSideProps` for data that needs to be fresh on each request
- Use `getStaticPaths` for dynamic routes with static generation
- Implement proper error handling for data fetching
- Use SWR or React Query for client-side data fetching
- Implement proper loading states and error boundaries

## Performance Optimization
- Use `next/image` for optimized image loading
- Implement proper code splitting with dynamic imports
- Use `next/dynamic` for component-level code splitting
- Implement proper caching strategies
- Use `next/head` for proper SEO and meta tags
- Optimize bundle size with proper imports and tree shaking

## SEO & Meta Tags
- Use `next/head` for page-specific meta tags
- Implement proper Open Graph and Twitter Card meta tags
- Use structured data for better search engine understanding
- Implement proper canonical URLs and sitemaps
- Use `next-seo` library for comprehensive SEO management
- Test SEO implementation with proper tools

## Styling & CSS
- Use CSS Modules for component-scoped styling
- Implement proper global styles in `_app.tsx`
- Use styled-components or emotion for dynamic styling
- Implement proper responsive design with CSS Grid and Flexbox
- Use CSS custom properties for theming
- Support dark mode with proper CSS variables

## API Routes
- Use the `pages/api` directory for API endpoints
- Implement proper HTTP methods and status codes
- Use proper request validation and error handling
- Implement proper authentication and authorization
- Use middleware for common functionality
- Handle CORS and security headers properly

## Authentication & Security
- Implement proper authentication with NextAuth.js or similar
- Use secure session management and JWT tokens
- Implement proper CSRF protection
- Use environment variables for sensitive configuration
- Implement proper input validation and sanitization
- Use HTTPS in production and proper security headers

## Deployment & Production
- Use Vercel for optimal Next.js deployment
- Implement proper environment variable management
- Use proper build optimization and compression
- Implement proper monitoring and error tracking
- Use proper CDN configuration for static assets
- Monitor performance and Core Web Vitals

## Testing
- Write unit tests for components and utilities
- Use Jest and React Testing Library for testing
- Implement integration tests for API routes
- Test both client and server-side functionality
- Mock external dependencies in tests
- Use proper test coverage and CI/CD integration

## TypeScript Integration
- Use TypeScript for all Next.js projects
- Define proper types for API responses and props
- Use proper type definitions for Next.js specific features
- Implement proper error handling with TypeScript
- Use proper type guards and type assertions
- Leverage TypeScript's strict mode for better type safety

## Internationalization
- Use `next-i18next` for internationalization
- Implement proper locale routing and detection
- Use proper translation management
- Implement proper date and number formatting
- Test with different locales and languages
- Use proper SEO for multilingual sites

