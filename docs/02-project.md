# Module 2 — Create the project

## 1. Scaffold from Microsoft's official template

Code App projects start from a Vite + React + TypeScript template hosted by Microsoft on GitHub:

+BQ+BQ+BQ+bash
npx degit github:microsoft/PowerAppsCodeApps/templates/vite my-first-code-app
cd my-first-code-app
npm install
+BQ+BQ+BQ+

You now have a completely ordinary React web app on disk — not yet registered in Power Platform.

## 2. Open in VS Code

+BQ+BQ+BQ+bash
code .
+BQ+BQ+BQ+

Take a quick look at the structure: +BQ+src/+BQ+ holds your React components, and +BQ+package.json+BQ+ contains the dev and build scripts.

## 3. Initialize as a Code App

+BQ+BQ+BQ+bash
pac code init --displayName "My First Code App"
+BQ+BQ+BQ+

This command:

- registers app metadata (name, build path, entry point)
- links the project to the environment you selected in module 1

With optional parameters you can control everything:

+BQ+BQ+BQ+bash
pac code init \
  --displayName "My First Code App" \
  --description "Workshop app built with React" \
  --environment https://<your-environment>.crm.dynamics.com
+BQ+BQ+BQ+

> 📝 **Note:** starting with the Power Apps client library for code apps v1.0.4+, there is also an npm-based CLI (+BQ+pa+BQ+) that will eventually replace the +BQ+pac code+BQ+ commands. This workshop uses the classic +BQ+pac code+BQ+ workflow for init/publish because it matches most existing material — and the +BQ+pa+BQ+ CLI in module 8 for data sources.

## 4. Commit the initial project

If you started from the workshop repository, commit now:

+BQ+BQ+BQ+bash
git add .
git commit -m "chore: scaffold code app from vite template"
git push origin main
+BQ+BQ+BQ+

✅ **Checkpoint:** the project exists, is linked to the environment, and is in Git.
