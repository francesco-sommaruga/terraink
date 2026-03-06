# CLAUDE.md — TerraInk

## Quick Reference

- **Package manager**: npm (or bun). Run `npm install` to set up.
- **Dev server**: `npm run dev` (Vite)
- **Build**: `npm run build` (Vite production build)
- **Typecheck**: `npm run typecheck` (`tsc --noEmit`)
- **No test suite** configured yet.

## Known Issues

- `npm run typecheck` reports pre-existing errors in `src/features/map/infrastructure/maplibreStyle.ts` (string literal types vs maplibre-gl enums). The build succeeds regardless since `strict: false` in tsconfig.

## Architecture

See `agent.md` for the full architecture guide. Key points:

- **Feature-based + Hexagonal/Clean** architecture under `src/features/`
- Four layers per feature: `domain/`, `application/`, `infrastructure/`, `ui/`
- Cross-cutting: `core/` (ports/adapters/config), `shared/` (utils/geo/ui), `data/` (static JSON), `styles/` (global CSS)
- State management via `PosterContext` (React Context + useReducer)
- All env vars accessed only through `src/core/config.ts`
- Use `@/` alias for cross-feature imports

## Environment

- Copy `.env.example` to `.env` and fill in values
- This fork points `VITE_REPO_URL` and `VITE_REPO_API_URL` to `francesco-sommaruga/terraink`

## Conventions

- New files must be `.ts` / `.tsx`
- React components: `PascalCase.tsx`, Hooks: `useCamelCase.ts`, Utilities: `camelCase.ts`
- Port interfaces use `I` prefix (e.g., `ICache`, `IHttp`)
- CSS classes: `kebab-case`
- Responsive breakpoints at `<=980px` and `<=760px`
