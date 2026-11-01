# Module 4 — Build a real app: React for Studio makers

Until now your app has been a heading and a counter button. In this module you build a **real app UI**: the Workshop Tasks app — a task list with a form, validation, and live counters. There is no data source yet (module 9 connects it to Dataverse or SharePoint); today the tasks live in memory so you can focus on React itself.

If you come from canvas apps and Power Apps Studio, here's the good news: **you already know these concepts — React just calls them different names.** This module is a translation guide, not a new language.

## 1. Your mental model, translated

| Power Apps Studio | React / Code App | Notes |
|---|---|---|
| Screen | Component | An app is a *tree* of components; a "screen" is just a top-level one |
| Control (Button, TextInput, Label) | JSX element | `<button>`, `<input>`, `<label>` — or a component you built yourself |
| Properties panel | Props | Inputs a parent passes down to a component |
| `OnSelect` / `OnChange` | `onClick` / `onChange` | Event handlers are ordinary functions |
| `UpdateContext` / `Set` | `useState` | State scoped to a component instead of a screen |
| `Navigate()` | Render a different component | There is no built-in "screen" concept — you decide |
| Gallery + `Items` | `array.map()` | Render one component per item |
| `Filter()` / `Sort()` | `.filter()` / `.sort()` | Client-side only here — module 9 shows the *delegated* version |
| `App.OnStart` | `useEffect` (on mount) | Run code when the app loads |
| `Patch()` / `Remove()` | generated service calls | Covered in module 9 |
| `Notify()` | your own state-driven banner | React ships nothing — you build it, which is the point |

> ⚠️ **The one real difference:** in Studio, formulas re-evaluate automatically when something changes. In React *you* own the state: nothing happens until you update it. More work — and far more control.

## 2. Components are your new controls

A component is a reusable piece of UI — like a custom control you can drop anywhere. It takes **props** (the properties you'd normally set in the panel) and returns markup:

```tsx
// src/components/TaskCard.tsx
export type Task = {
  id: string;
  title: string;
  done: boolean;
};

type TaskCardProps = {
  task: Task;
  onToggle: (id: string) => void;
  onDelete: (id: string) => void;
};

function TaskCard({ task, onToggle, onDelete }: TaskCardProps) {
  return (
    <li>
      <label>
        <input
          type="checkbox"
          checked={task.done}
          onChange={() => onToggle(task.id)}
        />
        <span style={{ textDecoration: task.done ? "line-through" : "none" }}>
          {task.title}
        </span>
      </label>
      <button onClick={() => onDelete(task.id)}>🗑️</button>
    </li>
  );
}

export default TaskCard;
```

Three things to notice:

- `task.done ? "line-through" : "none"` — that's your `If()`, in TypeScript clothes.
- The component *receives* `onToggle` and `onDelete` as props and just calls them — like a custom control raising `OnSelect` for the parent to handle.
- The component never edits `task` itself. **State lives above, components below.** This rule ("lifting state up") is what keeps apps sane as they grow.

## 3. State: your UpdateContext, one component at a time

`useState` returns a value and its setter — like a screen variable, but scoped to the component:

```tsx
const [title, setTitle] = useState("");   // like UpdateContext({ title: "" })
```

- `title` — the current value
- `setTitle("...")` — the **only** way to change it; plain assignment doesn't exist in React
- changing state automatically re-renders the component, like a screen refreshing after `UpdateContext`

An input wired to state like this:

```tsx
<input value={title} onChange={(e) => setTitle(e.target.value)} />
```

is called a **controlled component** — the React sibling of a TextInput bound with `Default` + `OnChange`.

## 4. Galleries are `.map()`

A Gallery renders `Items` into repeated rows. In React you map over any array:

```tsx
{tasks.map((task) => (
  <TaskCard key={task.id} task={task} onToggle={toggle} onDelete={remove} />
))}
```

Two rules that save you an afternoon:

1. Every item needs a unique `key` — like the ID column of a Gallery.
2. `.filter()` before `.map()` is exactly `Filter(Items, ...)` on a gallery — but only for local data. For real data sources, filtering is **delegated** (module 9).

## 5. Build it: the Workshop Tasks UI

Create two components and rewrite `App.tsx`. Work in small steps and watch hot reload after each one.

### Step 1: `src/components/TaskCard.tsx`

Use the component from section 2.

### Step 2: `src/components/TaskForm.tsx`

```tsx
import { useState } from "react";

type TaskFormProps = {
  onAdd: (title: string) => void;
};

function TaskForm({ onAdd }: TaskFormProps) {
  const [title, setTitle] = useState("");
  const [error, setError] = useState("");

  const submit = (e: React.FormEvent) => {
    e.preventDefault(); // don't reload the page
    if (title.trim().length < 3) {
      setError("Title must be at least 3 characters");
      return;
    }
    onAdd(title.trim());
    setTitle("");
    setError("");
  };

  return (
    <form onSubmit={submit}>
      <input
        value={title}
        onChange={(e) => setTitle(e.target.value)}
        placeholder="New task…"
      />
      <button type="submit">Add</button>
      {error && <p style={{ color: "crimson" }}>{error}</p>}
    </form>
  );
}

export default TaskForm;
```

- `e.preventDefault()` stops the browser from reloading the page. Your form behaves like a Studio form: nothing is submitted anywhere unless you say so.
- `{error && <p …>}` renders nothing while `error` is an empty string — conditional output without an `If` wrapper.

### Step 3: `src/App.tsx`

```tsx
import { useState } from "react";
import TaskCard, { type Task } from "./components/TaskCard";
import TaskForm from "./components/TaskForm";

function App() {
  const [tasks, setTasks] = useState<Task[]>([]);

  const addTask = (title: string) => {
    setTasks([...tasks, { id: crypto.randomUUID(), title, done: false }]);
  };

  const toggle = (id: string) => {
    setTasks(tasks.map((t) => (t.id === id ? { ...t, done: !t.done } : t)));
  };

  const remove = (id: string) => {
    setTasks(tasks.filter((t) => t.id !== id));
  };

  const done = tasks.filter((t) => t.done).length;

  return (
    <main style={{ maxWidth: 480, margin: "2rem auto", fontFamily: "sans-serif" }}>
      <h1>Workshop Tasks</h1>
      <p>
        {done} of {tasks.length} done
      </p>
      <TaskForm onAdd={addTask} />
      <ul style={{ listStyle: "none", padding: 0 }}>
        {tasks.map((t) => (
          <TaskCard key={t.id} task={t} onToggle={toggle} onDelete={remove} />
        ))}
      </ul>
    </main>
  );
}

export default App;
```

Read the handlers as Power Fx:

- `setTasks([...tasks, newTask])` — copy the array and append. State is **replaced, never mutated**: `tasks.push(...)` does nothing useful in React.
- `tasks.map((t) => (t.id === id ? { ...t, done: !t.done } : t))` — a `Patch` for a whole collection: copy every row, change the one field, leave the rest untouched.
- `const done = tasks.filter((t) => t.done).length` — recomputed on every render, exactly like a label with `CountRows(Filter(...))`.

### Step 4: Use it

`npm run dev`, add a task, tick it off, delete it. The counters update instantly — no publish needed. Local Play gives you the same "edit and immediately test" feeling as Studio preview, minus the save dialog.

## 6. Debugging without the App Checker

| Tool | What it gives you |
|---|---|
| `console.log(tasks)` + browser DevTools | Inspect any value — your new "View table" |
| Red squiggles + the Problems panel | TypeScript errors are the new "formula errors" — hover for a plain-language explanation |
| React Developer Tools (browser extension) | Inspect the component tree and each component's props/state — like screens and controls |

## 7. Where to go deeper

- [react.dev — Learn React](https://react.dev/learn) — the official tutorial; worth 60 minutes of anyone's time
- [Fluent UI React Components](https://react.fluentui.dev) — Microsoft's design system; drop-in components for a Power Apps look-and-feel
- [microsoft/PowerAppsCodeApps](https://github.com/microsoft/PowerAppsCodeApps) — official Code App samples

✅ **Checkpoint:** you can add a task via a validated form, tick it done, and delete it — with the UI split into reusable components (`TaskForm`, `TaskCard`), all hot-reloading locally. Exercise 3 makes you build it yourself from scratch.
