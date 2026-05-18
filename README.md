# Git Branching & Merging — Full Tutorial

Hey! Welcome to this hands-on Git tutorial. By the end of this, you'll be comfortable creating branches, merging code, resolving conflicts, and keeping a clean history with rebase. Each lesson builds on the last, and there's a mini project at the end to tie it all together.

Take it one lesson at a time — you've got this!

---

## Lessons

| # | Topic | What You'll Learn |
|---|-------|-------------------|
| [Lesson 1](lesson-1.md) | Branches — Create, Switch, Delete | How to isolate your work safely |
| [Lesson 2](lesson-2.md) | Merging — Fast-forward & 3-way | How to bring branches back together |
| [Lesson 3](lesson-3.md) | Merge Conflicts — Cause & Resolve | How to handle and fix conflicts like a pro |
| [Lesson 4](lesson-4.md) | Rebase — Clean Linear History | How to keep your history neat and readable |
| [Mini Project](mini-project.md) | Blog Site — Full Workflow | Apply everything in a real-world scenario |

---

## Learning Path

```
Lesson 1 --> Lesson 2 --> Lesson 3 --> Lesson 4 --> Mini Project
(Branches)   (Merging)   (Conflicts)   (Rebase)    (Put it all together)
```

Each lesson has:
- A clear explanation of the concept
- Visual diagrams to make it click
- All the commands you need
- Hands-on tasks to practice

---

## Quick Reference Cheatsheet

Keep this handy while you work through the lessons.

```bash
# -- Branches --------------------------------------------------
git branch                          # list all branches (* = current)
git checkout -b feature/x           # create + switch to new branch
git switch -c feature/x             # same thing, modern syntax
git branch -d feature/x             # delete branch (safe)
git branch -D feature/x             # force delete (even if unmerged)
git push origin feature/x           # push branch to remote
git push origin --delete feature/x  # delete branch from remote

# -- Merging ---------------------------------------------------
git checkout main
git merge feature/x                 # merge feature into main
git merge --no-ff feature/x         # always create a merge commit
git merge --abort                   # cancel merge (on conflict)

# -- Rebase ----------------------------------------------------
git checkout feature/x
git rebase main                     # replay commits on top of main
git rebase --continue               # continue after resolving conflict
git rebase --abort                  # cancel and restore original state

# -- Conflict Helpers ------------------------------------------
git status                          # see which files are conflicted
git diff                            # inspect conflict markers
git log --oneline --graph --all     # visualize full branch history
```

---

## How to Use This Tutorial

1. Start with **Lesson 1** — don't skip ahead
2. Read the explanation, then run the commands yourself
3. Complete the tasks before moving on
4. Use the cheatsheet above whenever you need a reminder
5. Finish with the **Mini Project** to solidify everything

> Pro tip: The best way to learn Git is to break things and fix them. Don't be afraid to experiment in a test repo!
# git-workflows
