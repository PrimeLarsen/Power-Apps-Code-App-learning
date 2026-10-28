# Exercise 1 — First App Loop (45 min)

**Goal:** From an empty folder to a published app in Power Apps.

1. Scaffold the project: `npx degit github:microsoft/PowerAppsCodeApps/templates/vite todo-app && cd todo-app && npm install`
2. Sign in: `pac auth create`
3. Select the environment: `pac env list` → `pac env select --environment <id>`
4. Initialize: `pac code init --displayName "Todo Workshop App"`
5. Run locally: `npm run dev` → open Local Play
6. Change the heading in `src/App.tsx` and confirm hot reload works
7. Build & publish: `npm run build` → `pac code push`
8. Open the URL from the output and play the app

**Definition of done:** a colleague can open your app via a shared link.

---

## Bonus

- Add an input box + button that adds items to a list (useState array)
- Show the count of completed items
