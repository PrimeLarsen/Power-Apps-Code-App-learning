# Module 3 — Local development

## 1. Start the dev server

`BQ`bash
npm run dev
`BQ`

Vite starts a local development server. Open the URL shown as **Local Play**.

> 🌐 **Important:** open Local Play in the same browser profile where you're signed in to your Power Platform tenant — otherwise you'll get identity/connection errors. Allow local network access if the browser prompts you (Chromium-based browsers can block local endpoints).

## 2. Make your first change

Open the main component in `src/` and make a small, visible change — for example:

`BQ`tsx
<h1>Hello from our first Code App! 👋</h1>
`BQ`

Save. Vite reloads automatically (hot reload) — which is the whole point: **edit code, see the result instantly.**

## 3. Build a small feature (10 min)

Add a button with state, for example in `src/App.tsx`:

`BQ`tsx
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <h1>Code App Counter</h1>
      <button onClick={() => setCount(count + 1)}>
        Clicked {count} times
      </button>
    </div>
  );
}

export default App;
`BQ`

## 4. Commit as you go

`BQ`bash
git switch -c feature/counter
git add .
git commit -m "feat: add counter component"
`BQ`

## 5. Troubleshooting 🔧

| Problem | Solution |
|---|---|
| Local Play won't load | Same browser profile as tenant login; check local network access permission |
| Build fails | `npm install`, check TypeScript errors |
| Auth errors | `pac auth list` → `pac auth select` |
| Wrong environment | `pac env select --environment <id>` |

✅ **Checkpoint:** the local dev loop works end to end.
