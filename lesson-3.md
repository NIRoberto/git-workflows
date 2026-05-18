# Lesson 3: Merge Conflicts

Don't let conflicts scare you — they're completely normal, and once you know how to handle them, they're no big deal. A conflict happens when two branches edit the **same line** of the same file. Git can't decide which version to keep, so it stops and asks you to decide.

---

## What a Conflict Looks Like

When Git hits a conflict, it marks the file like this:

```
<<<<<<< HEAD
This is the version from main
=======
This is the version from feature/x
>>>>>>> feature/x
```

- `<<<<<<< HEAD` — your current branch's version
- `=======` — the divider between the two versions
- `>>>>>>> feature/x` — the incoming branch's version

Your job is to pick what the final content should be and remove all the markers.

---

## How to Resolve a Conflict

1. Run `git status` to see which files are conflicted
2. Open each conflicted file
3. Decide what the final content should be (keep one side, keep both, or rewrite entirely)
4. Remove ALL conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
5. Stage the resolved file: `git add <file>`
6. Complete the merge: `git commit`

---

## Commands

```bash
git status                  # shows which files are conflicted
git diff                    # shows conflict markers in detail
git add <file>              # mark a conflict as resolved
git commit                  # finalize the merge
git merge --abort           # cancel the merge and go back to before it started
```

---

## Tasks — Trigger and Resolve a Conflict

- [ ] Create a repo, add `home.txt` with the line: `Welcome to my site`, commit on `main`
- [ ] Create branch `feature/update-home`, change that line to: `Welcome to my awesome site`, commit
- [ ] Switch back to `main`, change the same line to: `Welcome to the homepage`, commit
- [ ] Run `git merge feature/update-home` — you'll get a conflict
- [ ] Open `home.txt` and resolve it to: `Welcome to my awesome homepage`
- [ ] Remove all conflict markers, stage the file, and commit
- [ ] Run `git log --oneline --graph` to confirm the merge commit

---

## Bonus Task — Abort a Merge

- [ ] Trigger the same conflict again on a fresh branch
- [ ] This time, run `git merge --abort` instead of resolving
- [ ] Confirm you're back to the pre-merge state with `git status`

---

## Good to Know

- **Always start with `git status`** — it tells you exactly which files need attention and what state you're in
- **`git mergetool`** opens a visual diff editor if you prefer a GUI for resolving conflicts
- **Conflicts are not mistakes** — they just mean two people worked on the same thing. It happens on every real team.
- **Smaller, focused branches = fewer conflicts** — the more targeted your branch, the less likely it is to overlap with others

---

## Lesson Complete?

Before moving on, make sure you can answer these:

1. What causes a merge conflict?
2. What are the three conflict markers and what does each one mean?
3. What does `git merge --abort` do?

Almost there! Head to **[Lesson 4: Rebase -->](lesson-4.md)**
