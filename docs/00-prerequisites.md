# Module 0 — Prerequisites

Every participant should have the following on their own machine **before** the workshop (ideally as homework).

## 1. Install the tools

| Tool | Version | Notes |
|---|---|---|
| [Visual Studio Code](https://code.visualstudio.com) | latest | recommended IDE |
| [Node.js](https://nodejs.org) | LTS | includes +BQ+npm+BQ+ |
| [Git](https://git-scm.com) | latest | templates are pulled from GitHub |
| [Power Platform CLI](https://learn.microsoft.com/en-us/power-platform/developer/cli/introduction) (+BQ+pac+BQ+) | latest | easiest via the VS Code extension |
| .NET SDK | 8+ | only if +BQ+pac+BQ+ is installed as a .NET tool |

## 2. VS Code extensions

Install these from the Extensions marketplace:

- **Power Platform Tools** (also installs the PAC CLI + auth profiles)
- ESLint
- Prettier

## 3. Verify your installation

Open a terminal in VS Code and run:

+BQ+BQ+BQ+bash
node --version    # v20+ (LTS)
npm --version
git --version
pac --version      # Microsoft PowerPlatform CLI
+BQ+BQ+BQ+

If all four succeed, you're ready. If +BQ+pac+BQ+ fails, see Microsoft's installation guide (link above).

## 4. Licensing 🔑

Code Apps ultimately require:

- **Participants (developers):** Power Apps Premium, or pay-as-you-go enabled on the environment
- **End users of the app:** Power Apps Premium, an App Pass, pay-as-you-go, or auto-claim enabled

Check with your admin that the workshop environment is covered — otherwise publishing in module 4 will fail.

## 5. GitHub account

- Create a GitHub account (if you don't have one)
- Set up an SSH key or Personal Access Token so +BQ+git push+BQ+ works
- Fork the workshop repository, or use the one your workshop lead shared

✅ **Checkpoint:** all four version checks pass and you can push a commit to your fork.
