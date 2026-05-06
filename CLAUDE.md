# CLAUDE.md — Athletica

## Project Context

Before starting any task, read these files:
- `docs/STACK.md` — tech decisions
- `docs/FLOW.md` — app navigation flow
- `docs/DATABASE.md` — data model
- `docs/stories/INDEX.md` — feature list and status
- `docs/stories/[feature]/INDEX.md` — stories for the current feature

---

## Stack

| Layer | Technology |
|---|---|
| Mobile | React Native + Expo (development builds) |
| Backend | Express + TypeScript |
| ORM | Prisma |
| Database | Supabase (PostgreSQL) |
| Storage | Supabase Storage |
| Push | Firebase FCM |
| State | Zustand + React Query |
| Forms | React Hook Form + Zod |
| HTTP | Axios |

---

## Monorepo Structure

```
apps/api/     ← backend (Express)
apps/mobile/  ← frontend (Expo)
packages/shared-types/
docs/stories/[feature]/   ← one folder per feature
```

Always run backend commands from `apps/api/`.
Always run mobile commands from `apps/mobile/`.

---

## Branch Strategy

```
main   ← production — never touch directly
dev    ← base for all work
feat/  ← new features, branch from dev
fix/   ← bugfixes, branch from dev
chore/ ← setup, config, refactor
```

- Always branch from `dev`
- Never commit directly to `dev` or `main`
- Suggest branch name before starting
- Merge requests to `main` are done by the client only

---

## Stories Workflow

- Stories live in `docs/stories/[feature]/`
- Each feature folder has its own `INDEX.md` with status
- Status values: `TODO` → `IN PROGRESS` → `DONE` | `BLOCKED`
- Work one story at a time
- Update `INDEX.md` status before starting and when done
- Do not modify `DONE` stories — create a new one instead
- Stories not started yet can be updated
- If a story is too large, split it before starting

---

## Environments

- `dev` branch = development environment
- `main` branch = production environment
- All work goes to `dev` first
- Never add production-specific logic unless requested

---

## Expo Rules

- **Never use Expo Go**
- Always test with development builds:
  ```bash
  npx expo run:android   # Android emulator
  npx expo run:ios       # iOS simulator (Mac only)
  ```
- Re-run `npx expo run:android` only when changing `app.json` or native plugins
- Hot reload works after the first build — no need to recompile for JS changes

---

## Prisma Rules

- Never modify the database directly
- Every schema change requires a migration:
  ```bash
  npx prisma migrate dev --name describe-change
  ```
- Never edit migration files after they are applied

---

## Code Rules

- TypeScript strict mode — no `any`
- No business logic in controllers or components — use services and hooks
- Validate at boundaries: request bodies (Zod), never trust client data
- Errors: use `AppError` on backend, React Query error states on frontend
- No `console.log` in committed code
- Minimal diffs — avoid unrelated changes in the same commit

---

## Git Flow

1. Suggest branch name before starting
2. Explain the plan in 2-3 lines before coding
3. Suggest commit message after finishing
4. Provide TEST STEPS before any commit
5. Wait for validation before pushing
6. Keep commits focused on one story

**Commit format:**
```
feat: short description
fix: short description
chore: short description
```

---

## Test Steps Format

Before every commit, provide:
```
How to run: ...
What to test: ...
Expected result: ...
```

---

## What NOT to Do

- No Expo Go
- No direct DB changes (always Prisma migrations)
- No new libraries without asking first
- No AI features (post-MVP)
- No payment gateways (post-MVP)
- No Google Maps (post-MVP)
- No commits to `dev` or `main` directly
- No pushing without validation approval
- No large file rewrites unless necessary
- No renaming files/folders unless explicitly requested

---

## Communication Style

- Be concise
- No long summaries
- No repeating known context
- Ask before continuing if requirements are unclear
- Prioritize execution over explanation
