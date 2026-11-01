# Power Apps Code Apps — Workshop 🚀

A step-by-step repository that teaches a Power Platform developer team to build, version, and publish **Code Apps** — from an empty folder to a running app in Power Apps, with a proper ALM story on top.

> **What is a Code App?** A modern web app (React + Vite + TypeScript) that you develop locally in VS Code and publish into Power Platform — with full access to connectors, Dataverse, and Microsoft Entra ID authentication, without ever opening Power Apps Studio.

> **Who is this for?** Power Platform developers who are used to the low-code/no-code world — canvas apps, Power Apps Studio, flows. No prior React experience needed: module 4 translates the concepts you already know (screens, controls, galleries, variables) into components, props, and state.

## 🎯 Learning goals

By the end of the workshop, participants can:

1. Set up a complete dev environment (Node, Git, PAC CLI, VS Code)
2. Scaffold a Code App project from Microsoft's official template
3. Connect the project to a Power Platform environment
4. Develop and test locally with hot reload
5. Build a real, multi-component app UI in React — translating Studio concepts (screens, controls, galleries, variables) into components, props, and state
6. Publish the app to Power Apps with `pac code push`
7. Use Git branching, pull requests, and versioning as part of the app lifecycle
8. Set up CI/CD with GitHub Actions to build and deploy automatically
9. Connect a real data source — **Dataverse or SharePoint list** — and build a CRUD app on it
10. Use **GitHub Copilot** as a pair programmer to build faster — with review discipline

## 🗓️ Agenda (full day, ~7½ hours)

| Module | Topic | Time |
|---|---|---|
| 0 | Prerequisites & setup | 30 min |
| 1 | Environment connection & enabling Code Apps | 30 min |
| 2 | Project scaffolding + `pac code init` | 30 min |
| 3 | Local development (React + hot reload) | 45 min |
| 4 | **Build a real app: React for Studio makers** | 45 min |
| 5 | Build & publish to Power Apps | 45 min |
| 6 | Git for apps: branching, PRs, protected main | 45 min |
| 7 | Versioning: semver, tags, app versions, rollback | 30 min |
| 8 | CI/CD with GitHub Actions | 45 min |
| 9 | Connectors: build a CRUD app on Dataverse **or** SharePoint | 60 min |
| 10 | GitHub Copilot: build faster with an AI pair programmer | 30 min |
| — | Wrap-up & Q&A | 15 min |

## 📁 Repository structure

```
code-apps-workshop/
├── README.md                      ← you are here
├── .github/
│   └── workflows/
│       └── build-validation.yml   ← CI: build check on every push
├── docs/
│   ├── 00-prerequisites.md        ← tools & environment requirements
│   ├── 01-environment.md          ← enable Code Apps on the environment
│   ├── 02-project.md              ← scaffold the project + pac code init
│   ├── 03-local-dev.md            ← local development & testing
│   ├── 04-build-an-app.md         ← build a real app UI: React for Studio makers
│   ├── 05-publish.md              ← build & pac code push
│   ├── 06-git-for-apps.md         ← branching, PRs, code review
│   ├── 07-versioning.md           ← semver, git tags, rollback
│   ├── 08-ci-cd.md                ← automated builds & deploys
│   ├── 09-connectors.md           ← Dataverse or SharePoint CRUD
│   └── 10-copilot.md              ← GitHub Copilot as pair programmer
├── exercises/
│   ├── exercise-1.md              ← first app loop
│   ├── exercise-2.md              ← edit UI + republish
│   ├── exercise-3.md              ← build the Workshop Tasks app UI
│   ├── exercise-4.md              ← team flow with pull requests
│   ├── exercise-5.md              ← versioning & release flow
│   └── exercise-6.md              ← CRUD app on Dataverse or SharePoint
└── .gitignore
```

## 🚦 Getting started

Start in [docs/00-prerequisites.md](docs/00-prerequisites.md) and follow the modules in order 0 → 10. Each module ends with a ✅ checkpoint.

## 📚 Sources

- [Power Apps code apps overview — Microsoft Learn](https://learn.microsoft.com/en-us/power-apps/developer/code-apps/overview)
- [Connect your code app to data — Microsoft Learn](https://learn.microsoft.com/en-us/power-apps/developer/code-apps/how-to/connect-to-data)
- [Connect your code app to Dataverse — Microsoft Learn](https://learn.microsoft.com/en-us/power-apps/developer/code-apps/how-to/connect-to-dataverse)
- [Power Platform CLI — Microsoft Learn](https://learn.microsoft.com/en-us/power-platform/developer/cli/introduction)
- [PowerAppsCodeApps — official samples & templates (GitHub)](https://github.com/microsoft/PowerAppsCodeApps)
- [GitHub Copilot in VS Code — documentation](https://code.visualstudio.com/docs/copilot/overview)
