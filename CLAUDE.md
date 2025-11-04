# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Next.js 14 landing page project using the App Router, TypeScript, Tailwind CSS, and shadcn/ui components. The application features dark mode support via next-themes and is designed as a customizable landing page template.

## Development Commands

```bash
# Install dependencies
npm install

# Run development server (opens at http://localhost:3000)
npm run dev

# Build for production
npm run build

# Start production server
npm start

# Run ESLint
npm run lint
```

## Architecture

### App Router Structure

- **app/layout.tsx**: Root layout that wraps the app with the Providers component
- **app/providers.tsx**: Client-side providers, currently contains ThemeProvider for dark mode
- **app/page.tsx**: Main page that renders the MainContent component
- **app/globals.css**: Global styles and Tailwind CSS configuration with CSS variables for theming

### Component Organization

- **components/MainContext.tsx**: Main landing page component containing the entire page layout (header, hero section, features, CTA, footer)
- **components/ui/**: shadcn/ui components (button, card) - these should not be manually edited as they're managed by shadcn/ui CLI

### Utilities

- **lib/utils.ts**: Contains the `cn()` utility function for merging Tailwind classes using clsx and tailwind-merge

## Key Technologies

### shadcn/ui Integration

The project uses shadcn/ui for UI components. Configuration is in `components.json`:
- Components are installed in `components/ui/`
- Uses the "default" style with RSC (React Server Components) support
- Path aliases configured: `@/components`, `@/lib/utils`, `@/ui`, etc.

To add new shadcn/ui components, use:
```bash
npx shadcn@latest add <component-name>
```

### Theming

- Dark mode is implemented using `next-themes` with class-based theme switching
- Theme colors are defined as CSS variables in `app/globals.css`
- Tailwind is configured to use these CSS variables (see `tailwind.config.ts`)
- Theme toggle is in the header of MainContext.tsx using the `useTheme()` hook

### Path Aliases

TypeScript path aliases are configured in `tsconfig.json`:
- `@/*` maps to the root directory
- Allows imports like `import { Button } from "@/components/ui/button"`

## Client vs Server Components

- **app/providers.tsx** and **components/MainContext.tsx** are marked with `'use client'` because they use React hooks and client-side interactivity
- **app/layout.tsx** and **app/page.tsx** are Server Components by default
- The MainContent component uses `useState` and `useEffect` to handle hydration for the theme toggle

## Styling Conventions

- Uses Tailwind CSS utility classes for all styling
- Dark mode variants are applied with the `dark:` prefix
- Responsive breakpoints: `sm:`, `md:`, `lg:`, `xl:`
- The `cn()` utility function should be used when conditionally applying classes
