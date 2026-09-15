---
status: pending
title: Minimal Hello World App
---

## Goal
A single-page app whose home route displays a centered "Hello World" greeting with clean
Tailwind typography, a subtle gradient background, responsive sizing, and dark-mode support.
One route, no backend, no dependencies beyond the base stack.

## Current project state
The repository contains only `README.md`. No scaffold exists — the entire project
(package manifest, Vite config, TypeScript config, entry point, router setup, styles, route
files) must be created from scratch. There is no default starter content to remove, so no
cleanup step is needed beyond avoiding generated boilerplate copy in the home route.

## Files to add
1. `package.json` — npm scripts (dev/build/preview) and dependencies: react, react-dom,
   @tanstack/react-router; dev deps: vite, @vitejs/plugin-react, typescript, @types/react,
   @types/react-dom, tailwindcss, @tailwindcss/vite, @tanstack/router-plugin.
2. `index.html` — root HTML with a `#root` div and a module script pointing at `src/main.tsx`.
3. `vite.config.ts` — React plugin, Tailwind Vite plugin, TanStack Router plugin (file-based
   routing), and the `@/` alias mapped to `src/`.
4. `tsconfig.json` (plus `tsconfig.node.json` if needed) — strict mode, bundler resolution,
   `@/*` path alias.
5. `src/styles/global.css` — first line exactly `@import "tailwindcss";`.
6. `src/main.tsx` — imports the stylesheet once, creates the router from the generated route
   tree, renders `RouterProvider` into `#root`.
7. `src/routes/__root.tsx` — app shell: root route with an `Outlet`, full-height layout wrapper.
8. `src/routes/index.tsx` — the home route rendering the greeting.
9. `src/components/Greeting.tsx` — presentational component for the heading and subtext.
10. `.gitignore` — ignore `node_modules`, `dist`, and `src/routeTree.gen.ts`.

Note: `src/routeTree.gen.ts` is produced by the router plugin — never author or edit it.

## Step-by-step implementation
1. Create `package.json` with the dependencies listed above and `dev`, `build`, `preview`
   scripts. Outcome: `npm install` resolves the full toolchain.
2. Create `index.html` at the project root mounting `src/main.tsx`. Outcome: Vite has an entry
   document.
3. Create `vite.config.ts` registering the React, Tailwind, and TanStack Router plugins and the
   `@/` alias. Outcome: dev server starts and generates `src/routeTree.gen.ts` automatically.
4. Create `tsconfig.json` with strict TypeScript settings and the `@/*` path mapping matching
   the Vite alias. Outcome: editor and build agree on imports.
5. Create `src/styles/global.css` containing only the Tailwind import. Outcome: utility classes
   are available app-wide.
6. Create `src/routes/__root.tsx` defining the root route. The shell applies a minimum
   full-viewport height, a subtle light-to-dark gradient background (light palette by default,
   dark variants via `dark:`), default text colour, and antialiased text, then renders `Outlet`.
   Outcome: every route inherits the background and theme.
7. Create `src/components/Greeting.tsx` rendering an `h1` with "Hello World" using large
   responsive type (scaling up at `sm`/`md`/`lg`), tight tracking, semibold weight, and a short
   muted supporting line beneath it. Outcome: reusable, styling-only component.
8. Create `src/routes/index.tsx` registering the `/` route and rendering `Greeting` inside a
   flex container that centres content both horizontally and vertically with sensible padding.
   Outcome: the greeting is perfectly centred at all viewport sizes.
9. Create `src/main.tsx` importing `@/styles/global.css`, building the router from the generated
   route tree, and rendering `RouterProvider` inside `StrictMode`. Outcome: the app boots.
10. Create `.gitignore`. Outcome: build output and generated files stay untracked.

## Verification checklist
1. `npm install` completes without errors.
2. `npm run dev` starts and `src/routeTree.gen.ts` is generated.
3. Visiting `/` shows "Hello World" centred horizontally and vertically.
4. Resizing from mobile to desktop keeps the text centred and readable with no overflow.
5. Toggling the OS/browser dark mode preference switches background and text colours legibly.
6. `npm run build` succeeds with no TypeScript errors.
7. No unused starter/boilerplate content, no extra routes, no added dependencies.
