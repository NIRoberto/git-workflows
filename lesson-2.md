# Lesson 2: Merging

Great work making it to Lesson 2! You know how to create branches and work in isolation — now it's time to learn how to bring that work back together. That's merging.

Merging is how completed work gets integrated into the main codebase. It's one of the most common operations in any Git workflow, and understanding exactly what happens under the hood will save you a lot of confusion when things don't go as expected.

There are two types of merges in Git. They look different in your history and happen under different conditions. Let's break both of them down.

---

## Watch First

These videos do a great job of visualizing what actually happens during a merge — highly recommended before you run the commands yourself.

- **Git Merge Tutorial** (The Net Ninja, 8min)
  https://www.youtube.com/watch?v=XX-Kct0PfFc

- **Git Merging vs Rebasing** (Atlassian / Bitbucket, 5min)
  https://www.youtube.com/watch?v=CRlGDDprdOQ

- **Advanced Git Tutorial — Merge, Rebase, and More** (freeCodeCamp, 30min)
  https://www.youtube.com/watch?v=Uszj_k0DGsg

---

## Type 1: Fast-forward Merge

A fast-forward merge is the simplest possible merge. It happens when `main` hasn't received any new commits since you branched off. In this situation, there's no actual "merging" to do — Git just moves the `main` pointer forward to point at the tip of your feature branch.

Think of it like catching up. `main` was behind, and now it's caught up. No new commit is created.

```
Before:
main:       A ── B
                  \
feature/x:         C ── D

After (fast-forward):
main:       A ── B ── C ── D
                            ^
                           main now points here
```

```bash
git checkout main
git merge feature/x     # output: "Fast-forward"
```

This is the cleanest type of merge. The history stays perfectly linear — it looks like the feature was always part of `main`. You'll see this a lot when you're the only one working on a repo, or when you're the first to merge a feature.

---

## Type 2: Three-way Merge

A three-way merge happens when both `main` and your feature branch have diverged — meaning both have new commits that the other doesn't have. Git can't just move a pointer because there are two different histories to reconcile.

Git solves this by finding the **common ancestor** (the commit where the two branches split), comparing both branches to that ancestor, and combining the changes. The result is a new **merge commit** (`M`) that has two parents — one from each branch.

```
Before:
main:       A ── B ── E
                  \
feature/x:         C ── D

After (3-way merge):
main:       A ── B ── E ── M
                  \       /
feature/x:         C ── D
```

The merge commit `M` is special — it records the fact that two lines of history were joined at this point. You can see both parents with `git log --graph`.

```bash
git checkout main
git merge feature/x     # output: "Merge made by the 'ort' strategy"
                        # Git opens your editor for a merge commit message
```

---

## Commands

```bash
git merge feature/x               # merge feature/x into your current branch
git merge --no-ff feature/x       # force a merge commit even if fast-forward is possible
git merge --squash feature/x      # squash all feature commits into one before merging
git merge --abort                 # cancel an in-progress merge and restore the previous state
git log --oneline --graph --all   # visualize the full branch history including merge commits
```

**About `--no-ff` (no fast-forward):**
When you use `--no-ff`, Git always creates a merge commit even if a fast-forward was possible. This preserves the fact that a feature branch existed in your history. Many teams enforce this policy because it makes it easy to see exactly when and what was merged, and you can revert an entire feature with a single `git revert` on the merge commit.

**About `--squash`:**
`--squash` takes all the commits from your feature branch and combines them into a single staged change, which you then commit manually. This gives you a clean, single commit on `main` for the entire feature. The downside is you lose the individual commit history from the branch.

---

## What Happens to the Branch After Merging?

After a merge, the feature branch still exists — Git doesn't delete it automatically. The branch pointer just stays where it is. It's good practice to delete it once it's merged to keep your branch list clean:

```bash
git branch -d feature/x     # delete after merging
```

---

## Tasks

### Part A — Fast-forward Merge

- [ ] Create a new repo: `git init merge-practice && cd merge-practice`
- [ ] Create `index.txt`, add some text, and commit it on `main`
- [ ] Create branch `feature/nav`, add `nav.txt`, commit it
- [ ] Switch back to `main` — do NOT make any new commits here
- [ ] Run `git merge feature/nav` — the output should say **"Fast-forward"**
- [ ] Run `git log --oneline --graph` — notice the history is a straight line
- [ ] Delete the branch: `git branch -d feature/nav`

### Part B — Three-way Merge

- [ ] Make a new commit directly on `main` — edit `index.txt` and commit: `update: edit index`
- [ ] Create branch `feature/footer`, add `footer.txt`, commit it
- [ ] Switch back to `main` — this time `main` has moved ahead
- [ ] Run `git merge feature/footer` — Git will open your editor for a merge commit message
- [ ] Save the message and close the editor
- [ ] Run `git log --oneline --graph` — you should see the branching and merge commit clearly
- [ ] Compare this graph to Part A — notice the difference in shape

### Part C — Force a Merge Commit with --no-ff

- [ ] Create branch `feature/header`, add `header.txt`, commit it
- [ ] Switch to `main` (don't add any commits)
- [ ] Run `git merge --no-ff feature/header` — Git creates a merge commit even though fast-forward was possible
- [ ] Run `git log --oneline --graph` — you should see a merge commit even though the branches didn't diverge

---

## Good to Know

- **Fast-forward = cleaner, linear history** — but you lose the visual record that a feature branch existed. Good for small, personal changes.
- **Three-way merge = richer history** — you can see exactly when features were integrated and by whom. Better for team workflows.
- **The merge commit has two parents** — this is what makes it special. You can see both parents with `git log --graph` or `git show <merge-commit>`.
- **Always be on the target branch when merging** — you merge INTO your current branch. Switch to `main` first, then run `git merge feature/x`. A common mistake is running it from the wrong branch.
- **Merge conflicts can happen** — if both branches edited the same lines, Git will pause and ask you to resolve it manually. That's covered in detail in Lesson 3.

---

## Lesson Complete?

Before moving on, make sure you can answer these:

1. What condition causes a fast-forward merge?
2. What is a merge commit, what makes it different from a regular commit, and when does Git create one?
3. What does `--no-ff` do and why would a team enforce it?
4. After merging a feature branch, what should you do with it?

Ready for the tricky part? Head to **[Lesson 3: Merge Conflicts -->](lesson-3.md)**
