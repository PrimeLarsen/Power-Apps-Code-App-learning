# Exercise 3 — Build the Workshop Tasks app UI (45 min)

**Goal:** Build a complete, multi-component app UI in React, following module 4. No data source yet (that's exercise 6) — today the tasks live in memory, so focus on React, not plumbing.

## Part A: The components (25 min)

1. `src/components/TaskCard.tsx` — checkbox + title + delete button (props: `task`, `onToggle`, `onDelete`)
2. `src/components/TaskForm.tsx` — input + Add button, with validation: title must be at least 3 characters, error message shown inline
3. `src/App.tsx` — state and handlers: add, toggle, delete, and a done-counter ("X of Y done")

## Part B: Test the loop (10 min)

`npm run dev` → open Local Play → add, tick, delete — and try to submit an empty title to see your validation fire. Fix any TypeScript errors before moving on.

## Part C: Commit (10 min)

```bash
git switch -c feature/workshop-tasks-ui
git add .
git commit -m "feat: workshop tasks UI with form validation"
```

**Definition of done:** a colleague can add a task, tick it done, and delete it — and the counters update — without you running `pac code push`.

---

## Bonus (for the fast ones)

- Add a "Show all / Only open" toggle — like `Filter()` on a gallery (client-side `.filter()` is fine here, the data is local)
- Add a "Due" date to tasks and sort the list by it
- Move the counter into its own `TaskStats` component that receives the tasks as props
- Explain to your pair, in one sentence each: what is the React equivalent of `UpdateContext`, `Gallery`, and `Patch`?
