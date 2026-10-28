# Module 5 — Git for apps: branching, PRs & code review

## 1. Why this is gold for a team

Code Apps are plain text files (React/TypeScript). That means you can use **everything** you know from software development: branches, diffs, pull requests, code review, and CI. This is one of the biggest differences from classic studio-based development, where the +BQ+.msapp+BQ+ file is a binary blob.

| | Classic canvas app (studio) | Code App |
|---|---|---|
| Source format | Binary +BQ+.msapp+BQ+ | Text files (React/TS) |
| Diffs & review | Not practical | Full file diffs |
| Multiple developers | Merge pain in Studio | Git merge, one feature branch each |
| Rollback | Manual version restore | +BQ+git revert+BQ+ / redeploy any tag |

> ⚠️ **Known limitation:** Code Apps do **not** support Power Platform Git integration (yet) — use plain Git for source control. +BQ+pac code push+BQ+ is the deployment channel.

## 2. Recommended branching model (simple trunk-based)

+BQ+BQ+BQ+
main                → always releasable (protected branch)
  └── feature/xyz   → one branch per task
  └── fix/abc       → small fixes
+BQ+BQ+BQ+

+BQ+BQ+BQ+bash
git switch -c feature/todo-list
# ...code, commit...
git add .
git commit -m "feat: add todo list"
git push -u origin feature/todo-list
+BQ+BQ+BQ+

**Rules of the road (recommended for the team):**

1. Never commit directly to +BQ+main+BQ+
2. One feature branch per task, short-lived (days, not weeks)
3. Rebase onto +BQ+main+BQ+ before opening a PR to avoid noisy merges
4. Conventional commits (+BQ+feat:+BQ+, +BQ+fix:+BQ+, +BQ+chore:+BQ+) — they power the versioning module next

## 3. Protecting +BQ+main+BQ+ on GitHub

Settings → Branches → Add rule for +BQ+main+BQ+:

- ✅ Require a pull request before merging
- ✅ Require approval (1 reviewer is fine to start)
- ✅ Require status checks: select your CI build (module 7)
- ✅ Block force pushes

This makes "merge = reviewed" a guarantee, not a convention.

## 4. Pull request flow

1. Push your feature branch
2. On GitHub → **Compare & pull request**
3. Write a short description; link the task; add a reviewer
4. The reviewer comments / approves — small PRs get better reviews
5. Merge (squash merges keep history readable)
6. **After merge:** run +BQ+npm run build+BQ+ + +BQ+pac code push+BQ+ to deploy — or let CI do it (module 7)

## 5. Resolving a merge conflict (hands-on)

+BQ+BQ+BQ+bash
git switch main && git pull
git switch feature/my-branch
git rebase main
# conflict? open the file, pick the changes, then:
git add . && git rebase --continue
git push --force-with-lease
+BQ+BQ+BQ+

✅ **Checkpoint:** your branch is merged into +BQ+main+BQ+ via an approved pull request.
