# Lesson 4: Rebase

Welcome to the final lesson! Rebase is one of those Git features that feels confusing at first but becomes incredibly natural once it clicks. It's a powerful tool for keeping your history clean and readable — and it's used heavily in professional workflows.

The core idea is simple: instead of creating a merge commit to join two branches, rebase **replays your commits on top of another branch** as if you had started your work from there. The result is a perfectly linear history with no merge commits.

---

## Watch First

Rebase is one of those topics where seeing it visually first makes a huge difference. These videos are excellent.

- **Git Rebase Tutorial** (The Net Ninja, 9min)
  https://www.youtube.com/watch?v=f1wnYdLEpgI

- **Git Rebase vs Merge — Which is Better?** (Academind, 15min)
  https://www.youtube.com/watch?v=CRlGDDprdOQ

- **Git Rebase Explained** (freeCodeCamp, 20min)
  https://www.youtube.com/watch?v=_UZEXUrj-Ds

---

## How Rebase Works

When you run `git rebase main` from a feature branch, Git does the following:

1. Finds the common ancestor of your branch and `main` (the point where they diverged)
2. Temporarily sets your branch aside
3. Moves your branch pointer to the tip of `main`
4. Replays each of your commits one by one on top of `main`

The result is that your commits appear as if they were written after the latest commit on `main` — even if `main` moved forward while you were working.

```
Before rebase:
main:       A ── B ── E
                  \
feature/x:         C ── D

After: git rebase main (run from feature/x)
main:       A ── B ── E
                       \
feature/x:              C' ── D'
```

Notice that `C` and `D` become `C'` and `D'`. They contain the same changes, but they have **new commit hashes** because their parent commit changed. This is the key thing to understand about rebase — it rewrites history.

Now that `feature/x` is based on the latest `main`, merging it back is a clean fast-forward:

```
After: git checkout main && git merge feature/x
main:       A ── B ── E ── C' ── D'
```

A perfectly straight line. No merge commit. Clean and readable.

---

## Merge vs Rebase — Side by Side

```
# After merge (3-way):
main:    A ── B ── E ── M
                \       /
feature:         C ── D

# After rebase + fast-forward merge:
main:    A ── B ── E ── C' ── D'
```

Both approaches integrate the same changes. The difference is purely in how the history looks:

- **Merge** preserves the full picture — you can see exactly when branches diverged and when they were joined
- **Rebase** rewrites history to look linear — easier to read with `git log`, easier to bisect bugs, but loses the branching context

Neither is universally better. The right choice depends on your team's workflow and preferences.

---

## Commands

```bash
git checkout feature/x
git rebase main                 # replay feature/x commits on top of main

git rebase --continue           # after resolving a conflict, continue to the next commit
git rebase --abort              # cancel the rebase entirely and restore the original state
git rebase --skip               # skip the current commit (use carefully)

git rebase -i HEAD~3            # interactive rebase — rewrite, squash, or reorder the last 3 commits

git log --oneline --graph       # verify the clean linear history after rebasing
```

---

## Interactive Rebase — Bonus Feature

Interactive rebase (`-i`) is one of the most powerful Git tools for cleaning up your history before sharing it. It lets you rewrite, reorder, squash, or drop commits.

```bash
git rebase -i HEAD~3    # opens an editor showing your last 3 commits
```

In the editor, each commit is listed with a command prefix:

```
pick a1b2c3 add login page
pick d4e5f6 fix typo in login
pick g7h8i9 add logout button
```

You can change `pick` to:
- `reword` — keep the commit but edit the message
- `squash` (or `s`) — combine this commit with the one above it
- `fixup` (or `f`) — like squash but discard this commit's message
- `drop` (or `d`) — delete this commit entirely
- `edit` — pause here so you can amend the commit

This is how developers clean up messy "WIP" commits before opening a pull request.

---

## Handling Conflicts During Rebase

Unlike a merge (which resolves all conflicts in one go), rebase resolves conflicts **one commit at a time** as it replays each commit. This can feel more tedious but gives you finer control.

When a conflict occurs mid-rebase:

1. Git pauses and tells you which commit caused the conflict
2. Open the conflicted file and resolve it (same process as Lesson 3)
3. Stage the resolved file: `git add <file>`
4. Continue the rebase: `git rebase --continue`
5. Git moves to the next commit — repeat if there are more conflicts
6. When all commits are replayed, the rebase is complete

If at any point you want to give up and go back to where you started:

```bash
git rebase --abort      # restores everything to the state before you ran git rebase
```

---

## Tasks

### Main Task

- [ ] Create a new repo: `git init rebase-practice && cd rebase-practice`
- [ ] Make 2 commits on `main` — create `file-a.txt` and `file-b.txt` separately
- [ ] Create branch `feature/rebase-test`: `git checkout -b feature/rebase-test`
- [ ] Make 2 commits on the feature branch — create `feature-1.txt` and `feature-2.txt`
- [ ] Switch back to `main` and make 1 more commit — create `file-c.txt`
- [ ] Now `main` has moved ahead of where `feature/rebase-test` branched off
- [ ] Switch to `feature/rebase-test` and run `git rebase main`
- [ ] Run `git log --oneline --graph` — the history should be linear
- [ ] Switch to `main` and merge: `git merge feature/rebase-test` — it should fast-forward cleanly
- [ ] Run `git log --oneline` — confirm a straight, clean history

### Bonus — Rebase with a Conflict

- [ ] Create a new branch `feature/conflict-rebase`
- [ ] On both `main` and `feature/conflict-rebase`, edit the **same line** in the same file
- [ ] Run `git rebase main` from the feature branch
- [ ] Resolve the conflict, `git add`, then `git rebase --continue`
- [ ] Confirm the history is still clean and linear after

### Bonus — Interactive Rebase

- [ ] Make 3 messy commits on a branch (e.g., "wip", "fix typo", "actually done")
- [ ] Run `git rebase -i HEAD~3`
- [ ] Squash all three into a single clean commit with a proper message
- [ ] Run `git log --oneline` to confirm

---

## The Golden Rule of Rebase

> Never rebase a branch that other people are working on.

This is the most important rule in all of Git. Here's why:

Rebase rewrites commit hashes. When you rebase, your commits get new identities (`C'` instead of `C`). If a teammate has already pulled the original commits (`C`, `D`) and you then push the rebased versions (`C'`, `D'`), their local history will diverge from the remote. Git will see them as completely different commits, and the next `git pull` will create a mess of duplicate commits and conflicts that are very painful to untangle.

**Safe to rebase:** your own local branches that you haven't pushed yet, or branches that only you are working on.

**Never rebase:** `main`, `develop`, or any shared branch that others have pulled.

---

## When to Use Merge vs Rebase

| Situation | Recommended |
|-----------|-------------|
| Merging a completed feature into `main` on a team | Merge (with `--no-ff`) |
| Updating your local feature branch with latest `main` | Rebase |
| Cleaning up commits before opening a pull request | Interactive rebase |
| Working on a shared branch with teammates | Merge |
| Want to preserve the full branching history | Merge |
| Want a clean, readable, linear history | Rebase |

---

## Lesson Complete?

Before moving on, make sure you can answer these:

1. What does rebase actually do to your commits, step by step?
2. How is resolving a conflict during rebase different from during a merge?
3. Why should you never rebase a branch that other people are working on?
4. What is interactive rebase and what can you use it for?

You've finished all 4 lessons — now go put everything together in the **[Mini Project -->](mini-project.md)**
