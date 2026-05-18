# Lesson 2: Merging

Great work making it to Lesson 2! Now that you know how to create and switch branches, it's time to learn how to bring them back together. That's what merging is all about.

There are two types of merges in Git, and understanding the difference will save you a lot of confusion down the road.

---

## Type 1: Fast-forward Merge

A fast-forward merge happens when `main` hasn't changed since you branched off. There's nothing to "merge" — Git simply moves the `main` pointer forward to catch up with your branch. No extra commit is created.

```
Before:
main:       A ── B
                  \
feature/x:         C ── D

After (fast-forward):
main:       A ── B ── C ── D
```

```bash
git checkout main
git merge feature/x     # Git says: "Fast-forward"
```

This is the simplest and cleanest type of merge. You'll see it a lot when you're the only one working on a feature.

---

## Type 2: Three-way Merge

A three-way merge happens when both `main` and your feature branch have new commits since they diverged. Git can't just move a pointer — it has to combine two different histories. It does this by creating a **merge commit** (`M`) that has two parents.

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

```bash
git checkout main
git merge feature/x     # Git says: "Merge made by the 'recursive' strategy"
```

Git opens your editor to write a merge commit message. You can accept the default or write your own.

---

## Commands

```bash
git merge feature/x               # merge feature/x into your current branch
git merge --no-ff feature/x       # force a merge commit even if fast-forward is possible
git merge --abort                 # cancel an in-progress merge (useful on conflicts)
git log --oneline --graph --all   # visualize the full branch history
```

> Note: Use `--no-ff` when you want to preserve the fact that a feature branch existed, even if a fast-forward was possible. Many teams enforce this for a cleaner audit trail.

---

## Tasks

### Part A — Fast-forward Merge

- [ ] Create a new repo and commit a file on `main`
- [ ] Create branch `feature/nav`, add `nav.txt`, commit it
- [ ] Switch back to `main` and run `git merge feature/nav`
- [ ] Notice the output says **"Fast-forward"** — no merge commit was created
- [ ] Run `git log --oneline --graph` to confirm

### Part B — Three-way Merge

- [ ] Make a new commit directly on `main` (e.g., edit `index.txt`)
- [ ] Create branch `feature/footer`, add `footer.txt`, commit it
- [ ] Switch back to `main` and run `git merge feature/footer`
- [ ] This time Git creates a **merge commit** — write a message and save
- [ ] Run `git log --oneline --graph` and compare it to Part A

---

## Good to Know

- **Fast-forward = cleaner history**, but you lose the visual record that a branch existed
- **Three-way merge = richer history**, you can see exactly when features were integrated
- **The merge commit has two parents** — you can see this clearly in `git log --graph`
- **Always merge into the target branch** — switch to `main` first, then run `git merge feature/x`

---

## Lesson Complete?

Before moving on, make sure you can answer these:

1. What condition causes a fast-forward merge?
2. What is a merge commit and when does Git create one?
3. What does `--no-ff` do and why would you use it?

Ready for the tricky part? Head to **[Lesson 3: Merge Conflicts -->](lesson-3.md)**
