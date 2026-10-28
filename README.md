# Power Apps Code Apps — Workshop 🚀

A step-by-step repository that teaches a Power Platform developer team to build, version, and publish **Code Apps** — from an empty folder to a running app in Power Apps, with a proper ALM story on top.

> **What is a Code App?** A modern web app (React + Vite + TypeScript) that you develop locally in VS Code and publish into Power Platform — with full access to connectors, Dataverse, and Microsoft Entra ID authentication, without ever opening Power Apps Studio.

## 🎯 Learning goals

By the end of the workshop, participants can:

1. Set up a complete dev environment (Node, Git, PAC CLI, VS Code)
2. Scaffold a Code App project from Microsoft's official template
3. Connect the project to a Power Platform environment
4. Develop and test locally with hot reload
5. Publish the app to Power Apps with +BQ+pac code push+BQ+
6. Use Git branching, pull requests, and versioning as part of the app lifecycle
7. Set up CI/CD with GitHub Actions to build and deploy automatically
8. Connect a real data source — **Dataverse or SharePoint list** — and build a CRUD app on it

## 🗓️ Agenda (full day, ~7 hours)

| Module | Topic | Time |
|---|---|---|
| 0 | Prerequisites & setup | 30 min |
| 1 | Environment connection & enabling Code Apps | 30 min |
| 2 | Project scaffolding + +BQ+pac code init+BQ+ | 30 min |
| 3 | Local development (React + hot reload) | 45 min |
| 4 | Build & publish to Power Apps | 45 min |
| 5 | Git for apps: branching, PRs, protected main | 45 min |
| 6 | Versioning: semver, tags, app versions, rollback | 30 min |
| 7 | CI/CD with GitHub Actions | 45 min |
| 8 | Connectors: build a CRUD app on Dataverse **or** SharePoint | 60 min |
| — | Wrap-up & Q&A | 15 min |

## 📁 Repository structure

+BQ+BQ+BQ+
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
│   ├── 04-publish.md              ← build & pac code push
│   ├── 05-git-for-apps.md         ← branching, PRs, code review
│   ├── 06-versioning.md           ← semver, git tags, rollback
│   ├── 07-ci-cd.md                ← automated builds & deploys
│   └── 08-connectors.md           ← Dataverse or SharePoint CRUD
├── exercises/
│   ├── exercise-1.md              ← first app loop
│   ├── exercise-2.md              ← edit UI + republish
│   ├── exercise-3.md              ← team flow with pull requests
│   ├── exercise-4.md              ← versioning & release flow
│   └── exercise-5.md              ← CRUD app on Dataverse or SharePoint
└── .gitignore
+BQ+BQ+BQ+

## 🚦 Getting started

Start in [docs/00-prerequisites.md](docs/00-prerequisites.md) and follow the modules in order 0 → 8. Each module ends with a ✅ checkpoint.

## 📚 Sources

- [Power Apps code apps overview — Microsoft Learn](https://learn.microsoft.com/en-us/power-apps/developer/code-apps/overview)
- [Connect your code app to data — Microsoft Learn](https://learn.microsoft.com/en-us/power-apps/developer/code-apps/how-to/connect-to-data)
- [Connect your code app to Dataverse — Microsoft Learn](https://learn.microsoft.com/en-us/power-apps/developer/code-apps/how-to/connect-to-dataverse)
- [Power Platform CLI — Microsoft Learn](https://learn.microsoft.com/en-us/power-platform/developer/cli/introduction)
- [PowerAppsCodeApps — official samples & templates (GitHub)](https://github.com/microsoft/PowerAppsCodeApps)
