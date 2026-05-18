# Lesson 3: Merge Conflicts

Don't let conflicts scare you. Every developer who uses Git encounters them regularly — they're a completely normal part of collaborative work. Once you understand what they are and how to resolve them, they stop being stressful and become just another routine step.

A conflict happens when two branches have made changes to the **same part of the same file**, and Git can't automatically decide which version to keep. Git is smart enough to merge changes to different files, and even different parts of the same file, automatically. But when two changes overlap, it stops and hands the decision to you. That's the right call — only you know which version is correct.

---

## Watch First

These videos walk through real conflict scenarios step by step. Watching someone resolve a conflict before you do it yourself makes a big difference.

- **Resolving Merge Conflicts in Git** (The Net Ninja, 10min)
  https://www.youtube.com/watch?v=__cR7uPBOIk

- **Git Merge Conflicts — Full Tutorial** (freeCodeCamp, 30min)
  https://www.youtube.com/watch?v=HosPml1qkrg

- **How to Resolve Git Merge Conflicts** (Traversy Media, 15min)
  https://www.youtube.com/watch?v=xNVM5UxlFSA

---

## What Causes a Conflict?

Conflicts happen when:

1. **Two branches edit the same line(s) in the same file** — Git doesn't know which version to keep
2. **One branch edits a file and another branch deletes it** — Git doesn't know whether to keep or remove it
3. **Both branches add a file with the same name but different content** — Git doesn't know which one is correct

The most common case by far is #1 — two people (or two branches) editing the same lines.

---

## What a Conflict Looks Like

When Git hits a conflict, it pauses the merge and marks the conflicted sections directly inside the file using conflict markers:

```
<<<<<<< HEAD
Welcome to the homepage
=======
Welcome to my awesome site
>>>>>>> feature/update-home
```

Let's break down each marker:

- `<<<<<<< HEAD` — everything between this line and `=======` is the version from your **current branch** (the one you're merging into)
- `=======` — the divider separating the two conflicting versions
- `>>>>>>> feature/update-home` — everything between `=======` and this line is the version from the **incoming branch** (the one you're merging in)

Your job is to decide what the final content should look like, then remove all three markers. The file won't work correctly (and Git won't let you finish the merge) until every marker is gone.

---

## How to Resolve a Conflict — Step by Step

1. **Run `git status`** — it shows you exactly which files are in conflict, marked as `both modified`
2. **Open each conflicted file** in your editor
3. **Find the conflict markers** — your editor may highlight them automatically
4. **Decide on the final content** — you have three options:
   - Keep your version (delete the incoming section and markers)
   - Keep the incoming version (delete your section and markers)
   - Keep both (combine them manually and remove the markers)
   - Rewrite entirely (replace everything including markers with new content)
5. **Remove ALL conflict markers** — `<<<<<<<`, `=======`, `>>>>>>>` must all be gone
6. **Stage the resolved file**: `git add <file>`
7. **Complete the merge**: `git commit`

Git will pre-fill the commit message with something like `Merge branch 'feature/update-home'`. You can accept it or write your own.

---

## Commands

```bash
git status                      # see which files are conflicted (marked as "both modified")
git diff                        # see all conflict markers across all conflicted files
git add <file>                  # mark a specific file as resolved
git add .                       # mark all resolved files at once
git commit                      # finalize the merge after all conflicts are resolved
git merge --abort               # cancel the entire merge and go back to the state before it started
git log --oneline --graph       # verify the merge commit after resolving
```

---

## Using a Merge Tool

If you prefer a visual interface for resolving conflicts, Git has built-in support for merge tools:

```bash
git mergetool                   # opens your configured merge tool for each conflicted file
```

Popular options:
- **VS Code** — set it with `git config --global merge.tool vscode` and it opens a clean 3-panel view
- **vimdiff** — terminal-based, powerful but has a learning curve
- **IntelliJ / WebStorm** — excellent built-in merge tool if you use JetBrains IDEs

VS Code in particular is great for beginners — it shows your version, the incoming version, and the result side by side, with clickable buttons to accept one side or both.

---

## Tasks — Trigger and Resolve a Conflict

### Main Task

- [ ] Create a new repo: `git init conflict-practice && cd conflict-practice`
- [ ] Create `home.txt` with the single line: `Welcome to my site`
- [ ] Stage and commit it on `main`: `git commit -m "init: add home page"`
- [ ] Create branch `feature/update-home`: `git checkout -b feature/update-home`
- [ ] Change the line in `home.txt` to: `Welcome to my awesome site`
- [ ] Commit: `git commit -am "update: improve welcome message"`
- [ ] Switch back to `main`: `git switch main`
- [ ] Change the same line in `home.txt` to: `Welcome to the homepage`
- [ ] Commit: `git commit -am "update: rename to homepage"`
- [ ] Now merge: `git merge feature/update-home` — you'll get a conflict
- [ ] Run `git status` — confirm `home.txt` is listed as conflicted
- [ ] Open `home.txt` and resolve it to: `Welcome to my awesome homepage`
- [ ] Remove all conflict markers, save the file
- [ ] Stage it: `git add home.txt`
- [ ] Commit: `git commit` (accept the default merge message)
- [ ] Run `git log --oneline --graph` — confirm the merge commit with two parents

### Bonus Task — Abort a Merge

- [ ] Create a new branch `feature/abort-test`, change the same line again, commit
- [ ] Switch to `main`, change the same line differently, commit
- [ ] Run `git merge feature/abort-test` — conflict again
- [ ] This time, run `git merge --abort` instead of resolving
- [ ] Run `git status` — confirm you're back to a clean state on `main`

---

## Good to Know

- **Always run `git status` first** — it tells you exactly which files need attention, what state the merge is in, and what commands are available to you. It even prints helpful hints.
- **You can't accidentally lose work during a conflict** — Git has paused the merge and is waiting for you. Nothing is overwritten until you stage and commit. You're in full control.
- **Conflicts in binary files** (images, PDFs, etc.) can't be resolved with markers — Git will just tell you there's a conflict and you'll need to manually choose which version to keep using `git checkout --ours <file>` or `git checkout --theirs <file>`.
- **Smaller, focused branches = fewer conflicts** — the more targeted your branch, the less likely it is to overlap with other work. Long-lived branches that diverge significantly from `main` are the biggest source of painful conflicts.
- **Conflicts are not mistakes** — they're a sign that two people were working on the same area of the codebase. That's normal. The solution is communication and smaller branches, not avoiding Git.

---

## Lesson Complete?

Before moving on, make sure you can answer these:

1. What exactly causes a merge conflict?
2. What do the three conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) each represent?
3. What are the steps to resolve a conflict and complete the merge?
4. What does `git merge --abort` do, and when would you use it?

Almost there! Head to **[Lesson 4: Rebase -->](lesson-4.md)**
