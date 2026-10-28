# Module 4 — Build & publish to Power Apps

## 1. Build the production assets

```bash
npm run build
```

The script compiles TypeScript and places the Vite output in the configured build folder.

## 2. Publish to the environment

```bash
pac code push
```

On success, the PAC CLI returns a **Power Apps URL** — open it and test the published app.

The app now also appears on [make.powerapps.com](https://make.powerapps.com), where you can:

- play it (**Play**)
- share it with colleagues (**Share**)
- view version history and manage it

## 3. Share the app

In the Power Apps portal: select the app → **Share** → add users/groups.

> 🔑 Remember the licensing requirement: users need Power Apps Premium, an App Pass, pay-as-you-go, or auto-claim.

## 4. Publishing troubleshooting

| Error | Cause / solution |
|---|---|
| "Code apps not enabled" | An admin must enable Code Apps on the environment (module 1) |
| Push fails | Check license, permissions, and selected environment |
| Wrong app version | Run `npm run build` again, then `pac code push` |
| Wrong environment | `pac env select` before pushing |

## 5. The complete loop (memorize this!)

```bash
npm run dev      # develop locally
npm run build    # build
pac code push    # publish a new version
```

That's the entire Code App lifecycle in three commands. 🎉

✅ **Checkpoint:** a colleague can open your app via a shared link.
