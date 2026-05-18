# Lesson 3: Merge Conflicts ⚔️

A conflict happens when two branches edit the **same line** of the same file. Git can't decide which version to keep — you have to.

---

## What a Conflict Looks Like

```
<<<<<<< HEAD
This is the version from main
=======
This is the version from feature/x
>>>>>>> feature/x
```

- `<<<<<<< HEAD` — your current branch's version
- `=======` — the divider
- `>>>>>>> feature/x` — the incoming branch's version

---

## How to Resolve

1. Open the conflicted file
2. Decide what the final content should be (keep one, keep both, or rewrite)
3. Remove ALL conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
4. Stage the file: `git add <file>`
5. Complete the merge: `git commit`

---

## Commands

```bash
git status                  # shows which files are conflicted
git diff                    # shows conflict markers in detail
git add <file>              # mark conflict as resolved
git commit                  # finalize the merge
git merge --abort           # bail out and go back to before the merge
```

---

## ✅ Tasks — Trigger and Resolve a Conflict

- [ ] Create a repo, add a file `home.txt` with the line: `Welcome to my site`
- [ ] Commit on `main`
- [ ] Create branch `feature/update-home`, change that line to: `Welcome to my awesome site`, commit
- [ ] Switch back to `main`, change the same line to: `Welcome to the homepage`, commit
- [ ] Run `git merge feature/update-home` — you'll get a conflict
- [ ] Open `home.txt`, resolve it to: `Welcome to my awesome homepage`
- [ ] Remove conflict markers, stage, and commit
- [ ] Run `git log --oneline --graph` to confirm the merge commit

---

## ✅ Bonus Task — Abort a Merge

- [ ] Trigger the same conflict again on a fresh branch
- [ ] Run `git merge --abort` instead of resolving
- [ ] Confirm you're back to the pre-merge state with `git status`

---

## 💡 Tips

- Always run `git status` first — it tells you exactly which files need attention
- You can use a merge tool: `git mergetool` (opens a visual diff editor)
- Conflicts are normal — they just mean two people worked on the same thing
- Smaller, focused branches = fewer conflicts
