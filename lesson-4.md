# Lesson 4: Rebase

Welcome to the final lesson! Rebase is a powerful tool that gives you a clean, linear history by replaying your commits on top of another branch — no merge commits involved.

It takes a bit of getting used to, but once it clicks, you'll reach for it all the time.

---

## How Rebase Works

Instead of creating a merge commit, rebase picks up your commits and replays them as if you had started your branch from the latest point on `main`.

```
# Before rebase:
main:       A ── B ── E
                  \
feature/x:         C ── D

# After: git rebase main (from feature/x)
main:       A ── B ── E
                       \
feature/x:              C' ── D'
```

`C` and `D` are replayed as `C'` and `D'` — same changes, new commit hashes. Now `feature/x` is based on the latest `main`, and merging it back will be a clean fast-forward.

---

## Merge vs Rebase — Side by Side

```
# After merge:
main:    A ── B ── E ── M
                \       /
feature:         C ── D

# After rebase + merge:
main:    A ── B ── E ── C' ── D'
```

Rebase gives you a straight line. Merge preserves the full branching picture.

---

## Commands

```bash
git checkout feature/x
git rebase main               # replay feature commits on top of main

git rebase --continue         # after resolving a conflict mid-rebase
git rebase --abort            # cancel and go back to original state
git rebase --skip             # skip a commit that causes a conflict

git log --oneline --graph     # verify clean linear history
```

---

## Handling Conflicts During Rebase

Unlike merge (which resolves all conflicts at once), rebase resolves conflicts **one commit at a time**:

1. Rebase pauses at the conflicting commit
2. Fix the conflict in the file
3. `git add <file>`
4. `git rebase --continue` — moves on to the next commit
5. Repeat until all commits are replayed

---

## Tasks

- [ ] Create a repo, make 2 commits on `main` (`A`, `B`)
- [ ] Create `feature/rebase-test`, make 2 commits (`C`, `D`)
- [ ] Switch back to `main`, make 1 more commit (`E`)
- [ ] Switch to `feature/rebase-test` and run `git rebase main`
- [ ] Run `git log --oneline --graph` — history should be linear
- [ ] Switch to `main` and merge `feature/rebase-test` — it should fast-forward cleanly

---

## Bonus — Rebase with a Conflict

- [ ] On both `main` and `feature/rebase-test`, edit the **same line** in the same file
- [ ] Run `git rebase main` from the feature branch
- [ ] Resolve the conflict, `git add`, then `git rebase --continue`
- [ ] Confirm the history is still clean and linear after

---

## The Golden Rule of Rebase

> Never rebase a branch that other people are working on.

Rebase rewrites commit hashes. If a teammate has already pulled those commits, their history will diverge from yours and cause serious headaches. Only rebase your **own local branches** that haven't been shared yet.

---

## When to Use Merge vs Rebase

| Situation | Recommended |
|-----------|-------------|
| Shared or public branch | Merge |
| Local feature branch cleanup | Rebase |
| Want to preserve full branch history | Merge |
| Want a clean, linear history | Rebase |

---

## Lesson Complete?

Before moving on, make sure you can answer these:

1. What does rebase actually do to your commits?
2. How is resolving a conflict during rebase different from during a merge?
3. Why should you never rebase a shared branch?

You've finished all 4 lessons — now go put it all together in the **[Mini Project -->](mini-project.md)**
