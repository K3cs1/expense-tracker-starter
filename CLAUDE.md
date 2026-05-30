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

Single-page React app (Vite + React 19), split into four components:

- **`App`** — holds the `transactions` state (`{ id, description, amount, type, category, date }`). Passes data and callbacks down; contains no UI of its own beyond the page shell.
- **`Summary`** — receives `transactions`, computes `totalIncome`, `totalExpenses`, and `balance` internally, renders the three summary cards.
- **`TransactionForm`** — owns its own form state (`description`, `amount`, `type`, `category`). Calls `onAdd(transaction)` prop on submit.
- **`TransactionList`** — receives `transactions`, owns its own filter state (`filterType`, `filterCategory`), renders the filtered table.

The `categories` constant is duplicated in `TransactionForm` and `TransactionList` — a shared constants file doesn't exist yet.

**Known intentional bug** (course starter project): "Freelance Work" seed entry is categorised as `type: "expense"` despite being income.
