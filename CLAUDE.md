# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install      # install dependencies (required before first run)
npm run dev      # start dev server at http://localhost:5173
npm run build    # production build
npm run lint     # run ESLint
```

There is no test suite.

## Architecture

This is a single-page React app (Vite + React 19). All logic lives in one file: `src/App.jsx`.

**State** is managed with `useState` in the top-level `App` component:
- `transactions` — array of `{ id, description, amount, type, category, date }`. Amounts are stored as **strings** (not numbers), which causes the broken summary totals visible in the UI — `reduce` concatenates strings instead of summing them.
- Form state: `description`, `amount`, `type`, `category`
- Filter state: `filterType`, `filterCategory`

**Known intentional bugs** (this is a course starter project meant to be fixed):
- `amount` is stored and reduced as a string → summary totals are wrong (string concatenation instead of numeric addition)
- "Freelance Work" is typed `income` in description but stored as `type: "expense"` in seed data
- No delete functionality
- Minimal styling
