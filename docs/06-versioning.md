# Module 6 — Versioning: app versions, semver & rollback

## 1. Two layers of versioning

A Code App is versioned in **two places**, and a mature team keeps them in sync:

1. **Git** — the source of truth for code (tags, releases, commit history)
2. **Power Platform** — each +BQ+pac code push+BQ+ creates a new app version visible in make.powerapps.com

The golden rule: **never push from an uncommitted or untagged state.** If it's deployed, it must be traceable to a Git commit.

## 2. Semantic versioning for app releases

Version your releases as +BQ+MAJOR.MINOR.PATCH+BQ+:

| Segment | Bump when... | Example |
|---|---|---|
| +BQ+PATCH+BQ+ | Bug fixes, no behavior change | 1.0.0 → 1.0.1 |
| +BQ+MINOR+BQ+ | New feature, backwards compatible | 1.0.1 → 1.1.0 |
| +BQ+MAJOR+BQ+ | Breaking change or major milestone | 1.1.0 → 2.0.0 |

If you use conventional commits (module 5), the mapping is mechanical:

- +BQ+fix: ...+BQ+ → PATCH
- +BQ+feat: ...+BQ+ → MINOR
- +BQ+feat!:+BQ+ or breaking config/schema change → MAJOR

## 3. Tagging a release in Git

+BQ+BQ+BQ+bash
# annotate the release commit
git tag -a v1.1.0 -m "Release 1.1.0: todo list + sharing"
git push origin v1.1.0
+BQ+BQ+BQ+

On GitHub: **Releases → Draft a new release** → choose the tag → add release notes. Good release notes answer: *what changed, and what should a tester check first?*

## 4. Making the link explicit

Make the Git version visible in the app, e.g. via an environment variable baked in at build time:

+BQ+BQ+BQ+ts
const APP_VERSION = import.meta.env.VITE_APP_VERSION ?? "dev";
// render it in a footer:
<footer>v{APP_VERSION}</footer>
+BQ+BQ+BQ+

+BQ+BQ+BQ+bash
VITE_APP_VERSION=1.1.0 npm run build
pac code push
+BQ+BQ+BQ+

Now anyone seeing the app in Power Apps knows exactly which Git tag it came from. No more "which version is live?"

## 5. Rollback strategies

| Situation | Rollback |
|---|---|
| Bad publish to Power Platform | Restore an earlier app version in make.powerapps.com (versions list) |
| Bad code on +BQ+main+BQ+ | +BQ+git revert <commit>+BQ+ → rebuild → +BQ+pac code push+BQ+ |
| Need an old release back | +BQ+git switch --detach v1.0.0+BQ+ → rebuild → push |

Practice this deliberately — rollback is a muscle you want trained *before* the Friday-afternoon incident. 💪

## 6. Multi-environment promotion (the full picture)

+BQ+BQ+BQ+
dev environment   ← developers push here freely (pac code push)
test environment  ← only from CI, after PR merge
prod environment  ← only from CI, only from tagged releases (v*.*.*)
+BQ+BQ+BQ+

Rule of thumb: **manual pushes only to dev; everything further up moves through CI** (module 7).

✅ **Checkpoint:** you've tagged a release and can answer "which Git commit is running in test right now?"
