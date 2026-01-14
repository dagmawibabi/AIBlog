# AGENTS.md

This document provides guidelines for agents working on this SvelteKit blog codebase.

## Build, Lint, and Test Commands

```bash
# Development server with hot reload
pnpm dev

# Production build
pnpm build

# Preview production build locally
pnpm preview

# Type checking (svelte-check + TypeScript)
pnpm check

# Watch mode for type checking
pnpm check:watch

# Format code with Prettier
pnpm format

# Lint: Prettier check + ESLint
pnpm lint
```

**Note**: This project has no test framework configured. Do not add test commands.

## Code Style Guidelines

### TypeScript

- Use strict mode (`"strict": true` in tsconfig.json)
- Define interfaces for structured data (e.g., front matter, API responses)
- Use `$types` imports for SvelteKit types: `import type { PageServerLoad } from './$types';`
- Prefer explicit return types on server functions

### Svelte 5

- Use runes syntax: `$props()`, `$state()`, `$derived()`, `$effect()`
- Use `$bindable()` for two-way binding props
- Avoid legacy Svelte 4 reactivity (`export let`, `$:`)

### Formatting (Prettier)

- Use tabs for indentation (`"useTabs": true`)
- Single quotes for strings (`"singleQuote": true`)
- No trailing commas (`"trailingComma": "none"`)
- Print width: 100 characters
- Svelte files use Prettier plugin; TailwindCSS classes auto-sorted

### ESLint

- Follows flat config with TypeScript ESLint
- Svelte plugin enforces Svelte-specific rules
- Prettier config disables conflicting rules

### Imports

- Use `$lib` alias for internal imports: `import { cn } from '$lib/utils';`
- Group third-party imports before local imports
- Use named imports from UI libraries: `import { Button } from '$lib/components/ui/button';`
- Import types separately when possible

### Component Patterns (shadcn-svelte)

- Use `tailwind-variants` (`tv`) for component variants
- Follow pattern:

  ```svelte
  import { cn } from '$lib/utils.js';
  import type { HTMLButtonAttributes } from 'svelte/elements';

  let { class: className, children, ...restProps } = $props();
  ```

- Use `bits-ui` for primitive components (Button, Dialog, etc.)
- Export variant functions: `export const buttonVariants = tv({...})`

### Styling (TailwindCSS)

- Use CSS variables from `app.css` for colors: `bg-background`, `text-foreground`
- Dark mode: wrap dark styles with `.dark` class
- Use `cn()` utility for conditional classes
- Shadcn color palette: `primary`, `secondary`, `muted`, `destructive`, `accent`, `card`, `popover`
- Border radius: `sm`, `md`, `lg`, `xl` (uses `--radius` variable)

### Error Handling

- Use SvelteKit `error()` helper for HTTP errors:
  ```ts
  import { error } from '@sveltejs/kit';
  throw error(404, 'Blog not found');
  ```
- Wrap async operations in try/catch with logging
- Return proper status codes (400, 404, 500)

### Project Structure

```
src/
├── components/          # Shared Svelte components
├── lib/
│   ├── components/ui/   # shadcn-svelte UI components
│   ├── assets/          # Static assets
│   ├── utils.ts         # Utility functions (cn, etc.)
│   └── config.json      # Blog configuration
├── routes/
│   ├── api/             # API endpoints (+server.ts)
│   ├── blog/            # Blog pages
│   └── write/           # Blog editor
└── app.css              # Global styles + CSS variables
static/blogs/            # Markdown blog posts
```

### Blog Post Format

Markdown files in `static/blogs/` require front matter:

```yaml
---
title: Blog Title
date: 2025-01-15
category: 'Category'
description: 'Short description'
---
```

**Note**: If description contains apostrophes, use double quotes instead:

```yaml
description: "Here's a description with apostrophes"
```

### API Endpoints

- Place in `src/routes/api/[endpoint]/+server.ts`
- Use `POST`, `GET`, etc. named exports
- Return `json()` from `@sveltejs/kit`
- Access request body via `await request.json()`

### Dark Mode

- Use `mode-watcher` library: `import { toggleMode } from 'mode-watcher';`
- Toggle with button click handler
- CSS variables handle light/dark values automatically

### Utilities

- `cn()`: Merge Tailwind classes (clsx + tailwind-merge)
- Located in `src/lib/utils.ts`
- Always use for conditional class strings
