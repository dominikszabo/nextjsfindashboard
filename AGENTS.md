# AGENTS.md - Next.js Dashboard Codebase Guidelines

## Build & Development Commands

```bash
# Install dependencies (requires pnpm)
pnpm install

# Development server with Turbopack
pnpm dev

# Production build
pnpm build

# Start production server
pnpm start
```

### Testing
- Currently no testing framework is configured
- To add tests: consider Vitest (lightweight) or Jest with React Testing Library
- Single test commands will be available once a test framework is configured

### Linting & Formatting
- No ESLint or Prettier configured yet
- Recommended: Add ESLint with Next.js config and Prettier for formatting
- TypeScript strict mode is enabled (`strict: true` in tsconfig.json)

## Code Style Guidelines

### TypeScript
- **Strict mode enabled**: Use explicit types, avoid `any`
- **File extensions**: Use `.tsx` for React components, `.ts` for utilities
- **Imports**: Use path aliases (`@/` maps to project root)
  ```typescript
  import Component from '@/app/ui/component'
  ```
- **React Components**: Export as named exports, use function declaration syntax
- **Types**: Define in `app/lib/definitions.ts` for shared types

### React & Next.js
- **App Router**: All code uses App Router pattern (not Pages Router)
- **Server Components**: Default; use `'use client'` only for interactivity
- **Component structure**:
  ```typescript
  'use client' // or server component (no directive)
  
  import X from '@/path'
  
  export default function ComponentName({ props }) {
    return <JSX />
  }
  ```
- **Metadata**: Configure in `app/layout.tsx` for root layout

### Styling
- **Tailwind CSS**: Primary styling method
- **Utility-first**: Use atomic Tailwind classes
- **Component-specific CSS**: Create `*.module.css` files in component directories
- **Color palette**: Use project-defined colors from `tailwind.config.ts`
  - Blue: 400 (#2589FE), 500 (#0070F3), 600 (#2F6FEB)

### Naming Conventions
- **Components**: PascalCase (e.g., `Sidebar`, `RevenueChart`)
- **Files**: Match component names or use descriptive names (e.g., `button.tsx`)
- **Variables/Functions**: camelCase (e.g., `formatCurrency`, `currentPage`)
- **Types/Interfaces**: PascalCase with descriptive names (e.g., `Invoice`, `Customer`)
- **CSS Classes**: Tailwind utility classes; use `clsx()` for conditional classes

### Error Handling
- **Client-side**: Use try-catch blocks for async operations
- **Server-side**: Handle errors in route handlers
- **User feedback**: Show meaningful error states in UI
- **Validation**: Use Zod schemas (`zod` already in dependencies) for form validation

### Best Practices
1. **File organization**: Match route structure (e.g., `/users/page.tsx` for users page)
2. **Separation of concerns**: Keep data fetching in `app/lib/data.ts` or route handlers
3. **UI components**: Place in `app/ui/` directory, organized by feature
4. **Reusable utilities**: Add to `app/lib/utils.ts`
5. **Type safety**: Define types for all database records in `definitions.ts`
6. **Client-side state**: Use React hooks; consider use-debounce for search inputs

## Testing Strategy (Recommended)

When adding tests:
- **Unit tests**: Vitest for utility functions
- **Component tests**: Vitest + React Testing Library
- **E2E tests**: Playwright or Cypress for critical user flows
- **Test location**: `__tests__/` or `__stories__/` directories adjacent to files

## Commit Guidelines

- Use conventional commits: `feat:`, `fix:`, `docs:`, `chore:`, etc.
- Reference issues: `fixes #123`
- Keep commits focused on single changes

## Tools & Dependencies

- **Framework**: Next.js 15 (App Router)
- **_styling**: Tailwind CSS 3.4.17
- **TypeScript**: 5.7.3 with strict mode
- **Auth**: NextAuth 5.0.0-beta.25
- **Data validation**: Zod 3.25.17
- **Icon library**: Heroicons 2.2.0
- **Package manager**: pnpm (configure `onlyBuiltDependencies` for native modules)
