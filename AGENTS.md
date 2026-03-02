# AGENTS.md

## Cursor Cloud specific instructions

### Overview

This is **app-educacional**, a Next.js 14 educational platform (TypeScript) using Supabase as a hosted backend (auth + PostgreSQL). There is no local database or Docker dependency — only a single Next.js frontend service.

### Running the app

- `npm run dev` — starts the dev server on `http://localhost:3000`
- `npm run build` — production build (**currently fails** due to existing ESLint errors in `app/(dashboard)/academy/courses/[id]/page.tsx`; dev server works fine)
- `npm run lint` — runs ESLint (requires `.eslintrc.json` with `"extends": "next/core-web-vitals"`)

### Environment variables

Supabase credentials are required in `.env.local`. See `SETUP_GUIDE.md` for the project's Supabase URL and anon key. The two required variables are:

- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`

### Authentication

All dashboard routes (`/`, `/academy`, `/loja`, `/agenda`, `/nivel`) are protected by `AuthProvider` and redirect to `/login` without a valid Supabase session. A test account in the Supabase project is needed to access any page beyond login.

### Gotchas

- The repo originally had **no `.eslintrc.json`**, causing `next lint` to prompt interactively. The file must exist for non-interactive lint runs.
- The repo has **no `.gitignore`**. Be careful not to commit `node_modules/`, `.next/`, or `.env.local`.
- `npm run build` fails due to `@next/next/no-assign-module-variable` error in the course detail page — this is pre-existing.
