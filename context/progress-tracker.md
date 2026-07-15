# Progress Tracker

Update this file after every meaningful implementation
change.

## Current Phase

- In progress

## Current Goal

- Move to the next feature unit (see `context/feature-specs/02-editor.md`).

## Completed

- Design system and UI primitives (01-design-system.md): shadcn/ui initialized
  (`components.json`, `lib/utils.ts` with `cn()`), Button/Card/Dialog/Input/
  Tabs/Textarea/ScrollArea added, `lucide-react` installed, `app/globals.css`
  rebuilt to the dark-only palette from `context/ui-context.md`.

## In Progress

- None yet.

## Next Up

- 02-editor.md

## Open Questions

- [Any unresolved product or technical decisions]

## Architecture Decisions

- shadcn CLI resolved this project's `components.json` to the "base-nova"
  style, which composes on `@base-ui/react` rather than Radix — use the
  `render={<X/>}` prop for trigger/slot composition, not Radix's `asChild`.
- `app/globals.css` keeps shadcn's semantic variables (`--background`,
  `--card`, `--primary`, etc., required by unmodified `components/ui/*`
  files) but sources their values from the project-specific tokens defined
  in `context/ui-context.md` (`--bg-base`, `--text-primary`, `--accent-primary`,
  etc.) so there is one source of truth for the palette. Those project
  tokens are also exposed directly as Tailwind utilities (`bg-base`,
  `text-copy-primary`, `border-surface-border`, `text-brand`, `bg-accent-dim`, ...)
  per `code-standards.md`.
- App is dark-only: `.dark` class is applied permanently on `<html>` in
  `app/layout.tsx` (no theme toggle) since `components/ui/*` bake in extra
  `dark:` refinement classes that need the `.dark` ancestor to activate.

## Session Notes

- Local Node default (via nvm) is v18.17.0, but this Next.js version and the
  shadcn CLI require Node >=20 — use `nvm use 20.20.2` (or 22.15.0) when
  running `next dev`/`next build`/`npx shadcn`.
- Verified via typecheck (`npx tsc --noEmit`), `next build`, and a throwaway
  route exercising all 7 components + `cn()` + a lucide icon in the browser;
  the throwaway route was deleted after verification (not part of the diff).
