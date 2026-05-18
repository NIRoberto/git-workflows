# Lesson 1: Branches

Welcome to Lesson 1! This is where everything starts. Branches are one of Git's most powerful features — they let you work on new ideas, features, or fixes in complete isolation, without ever touching your stable `main` code.

Think of a branch as your own personal workspace. You can experiment freely, and when you're happy with the result, you bring it back.

---

## How Branches Work

When you create a branch, Git creates a new pointer to the current commit. From that point on, your changes and `main`'s changes are completely independent.

```
main:       A ── B
                  \
feature/x:         C ── D
```

- `A` and `B` are commits on `main`
- You branched off at `B` and made commits `C` and `D`
- `main` has no idea those commits exist — yet

When you're done, you merge `feature/x` back into `main` (covered in Lesson 2).

---

## Commands

```bash
# Viewing branches
git branch                          # list all local branches (* = you are here)
git branch -a                       # list local + remote branches

# Creating branches
git branch feature/login            # create branch (but stay on current)
git checkout -b feature/login       # create + switch in one step
git switch -c feature/login         # same thing, modern syntax (Git 2.23+)

# Switching branches
git checkout feature/login          # switch to existing branch
git switch feature/login            # modern way to switch

# Deleting branches
git branch -d feature/login         # safe delete (only if already merged)
git branch -D feature/login         # force delete (even if not merged)

# Working with remotes
git push origin feature/login           # push branch to remote
git push origin --delete feature/login  # delete branch from remote
```

---

## Tasks

Work through these in order. Each one builds on the last.

- [ ] Create a new repo: `git init branch-practice && cd branch-practice`
- [ ] Create `index.txt`, write a line of text, and commit it on `main`
- [ ] Create a new branch called `feature/about`
- [ ] Switch to `feature/about`, create `about.txt`, and commit it
- [ ] Switch back to `main` — notice that `about.txt` has disappeared (it's safe on the other branch!)
- [ ] Run `git log --oneline --graph --all` to see both branches side by side
- [ ] Delete the `feature/about` branch with `git branch -d feature/about`

---

## Good to Know

- **Branch naming conventions** — teams typically use prefixes like `feature/`, `fix/`, `hotfix/`, `chore/` to keep things organized. Example: `feature/user-auth`, `fix/login-bug`
- **`git branch` with no args** — the `*` next to a branch name shows where you currently are
- **Deleting a branch is safe** — it only removes the label (pointer). The actual commits stay in Git's history until they're garbage collected. Nothing is truly lost.
- **`git switch` vs `git checkout`** — both work, but `git switch` is the newer, cleaner command introduced in Git 2.23. Use whichever feels natural.

---

## Lesson Complete?

Before moving on, make sure you can answer these:

1. What does `git checkout -b feature/x` do in one step?
2. Why does `about.txt` disappear when you switch back to `main`?
3. What's the difference between `git branch -d` and `git branch -D`?

When you're confident — head to **[Lesson 2: Merging -->](lesson-2.md)**
