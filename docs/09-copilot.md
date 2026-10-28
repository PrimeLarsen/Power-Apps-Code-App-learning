# 09 — GitHub Copilot as your pair programmer 🤖

You don't have to write every line yourself. GitHub Copilot is built into VS Code and works directly in your Code App project — it's excellent for React/TypeScript scaffolding, and Code Apps are exactly the kind of modern TypeScript codebase it shines at.

## Why this fits this workshop

Code Apps are standard React + Vite + TypeScript. That means Copilot can help with:

- **Component scaffolding** — describe the component you want and let it draft the JSX + styling
- **Typing data models** — paste a JSON sample of your Dataverse/SharePoint rows and ask for an interface
- **Refactoring** — extract repeated UI into components, clean up hooks
- **Explaining unfamiliar code** — highlight the `CodeAppServices` usage and ask "what does this do?"
- **Writing tests and CI tweaks** — useful in modules 07 and 08

## Setup (2 minutes)

1. In VS Code, install the **GitHub Copilot** + **GitHub Copilot Chat** extensions
2. Sign in with your GitHub account (Copilot needs an appropriate license — check with your admin if in doubt)
3. That's it — suggestions appear as you type; `Tab` accepts, `Esc` dismisses
4. Open **Copilot Chat** (`Ctrl+Alt+I` / `Ctrl+Shift+I`) for conversation-style help

## How to prompt it well

Treat Copilot like a junior developer with infinite patience:

- **Give context**: reference actual files (`#file:App.tsx`) so suggestions match your project
- **Be specific**: "Add a delete button to each row in TaskList that calls the REST endpoint and refreshes the list" beats "add delete"
- **Iterate**: first answer is a draft — refine with follow-ups
- **Review everything**: it's your PR, your app, your responsibility

## Example: accelerate module 8

When you build the CRUD app, try this prompt in Copilot Chat:

```
Create a React component `TaskForm` for creating tasks. Fields: title (text), due date (date), status (choice: open/in_progress/done). Use the Dataverse Web API endpoint /api/data/v9.2/workshoptasks with the CodeAppServices helper from #file:CodeAppServices.ts.
```

Then review, adjust to your table's actual schema names, and test locally (`npm run start`) before publishing.

## Guardrails

- **Always review before committing** — Copilot can hallucinate API names or invent columns that don't exist in your table
- **Never paste secrets, connection strings, or auth profiles** into prompts
- Generated code still goes through the same **branch → PR → CI** flow from module 5 — Copilot doesn't skip ALM
- Generated code must comply with the same licenses and policies as your own code

## ✅ Checkpoint

- [ ] Copilot extensions installed and signed in
- [ ] You've used Copilot Chat on at least one component with a file reference
- [ ] You reviewed and adjusted at least one suggestion before committing

