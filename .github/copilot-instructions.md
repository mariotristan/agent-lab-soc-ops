# Soc Ops - Social Bingo Game AI Agent Instructions

## Mandatory Development Checklist
- [ ] `npm run lint` - ESLint passes (strict TypeScript rules)
- [ ] `npm run build` - TypeScript + Vite build succeeds  
- [ ] `npm run test` - All 21 unit tests pass
- [ ] Dev server running on http://localhost:5173/

## Architecture Overview

**Core Pattern**: Pure functional game logic separated from React UI state management.

- **Game Logic**: [`src/utils/bingoLogic.ts`](src/utils/bingoLogic.ts) - pure functions for board generation, square toggling, win detection
- **State Management**: [`src/hooks/useBingoGame.ts`](src/hooks/useBingoGame.ts) - React state + localStorage persistence
- **Component Flow**: `App.tsx` → conditional rendering between `StartScreen` and `GameScreen` + modal overlay

## Key Patterns

**Game State Flow:**
1. `generateBoard()` creates 5x5 grid with shuffled questions (center = free space)
2. `toggleSquare()` returns new board array (immutable updates) 
3. `checkBingo()` validates win conditions on every board change
4. `useBingoGame` orchestrates state + localStorage persistence

**Component Conventions:**
- Props are action-oriented: `onSquareClick`, `onReset`, `onDismiss`
- State lifting: `useBingoGame` hook provides all game state to `App.tsx`
- Pure components: Game components receive state, don't manage it

**Tailwind CSS 4 Usage:**
- Custom theme variables in [`src/index.css`](src/index.css) via `@theme {}` directive
- Semantic color names: `accent`, `marked`, `bingo` instead of generic blues/greens

## Custom Agent Integration

**Available Specialized Agents** (see [`.github/agents/`](.github/agents/)):
- `Quiz Master` - Generate themed bingo questions
- `TDD Red/Green/Refactor` - Test-driven development workflow  
- `Pixel Jam` - UI design iteration with visual feedback
- `UI Review` - Automated UX analysis using Playwright

**Deployment**: GitHub Pages auto-deploy on push to `main`. Uses `VITE_REPO_NAME` env var for correct base path.

## Critical Files for Changes
- Game behavior: Modify [`src/utils/bingoLogic.ts`](src/utils/bingoLogic.ts) + corresponding tests
- UI styling: Update [`src/index.css`](src/index.css) theme variables  
- Questions: Edit [`src/data/questions.ts`](src/data/questions.ts) array
- New game modes: Extend [`src/types/index.ts`](src/types/index.ts) `GameState` type
