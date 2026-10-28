# Exercise 4 — Versioning & release flow (30 min)

**Goal:** Make "which version is live?" an answerable question — and practice a rollback.

## Part A: Version the app

1. Add a version footer to your app (module 6, step 4):
   `BQ`ts
   const APP_VERSION = import.meta.env.VITE_APP_VERSION ?? "dev";
   `BQ`
2. Build with an explicit version and publish:
   `BQ`bash
   VITE_APP_VERSION=1.0.0 npm run build && pac code push
   `BQ`
3. Verify the version is visible in the running app in Power Apps

## Part B: Tag a release

1. Make one small `feat:` change and one `fix:` change (two commits, conventional messages)
2. Decide the correct next version number per semver rules and discuss in the group
3. Tag and push:
   `BQ`bash
   git tag -a v1.1.0 -m "Release 1.1.0"
   git push origin v1.1.0
   `BQ`
4. Create a GitHub Release from the tag with release notes

## Part C: Rollback drill 🚨

1. Break something on purpose (a `feat:` that crashes the app) and publish it
2. Roll back: `git revert <commit>` → rebuild → `pac code push`
3. Alternative: restore an earlier app version in make.powerapps.com
4. Debrief: which rollback path was faster, and when would you use each?

**Definition of done:** you can point at any running app and name the Git tag it came from.
