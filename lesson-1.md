# Lesson 1: Branches

Welcome to Lesson 1! Now that you have the fundamentals down, it's time to learn one of Git's most powerful and most-used features — branches.

Branches are what make Git truly great for real-world development. They let you work on a new feature, experiment with an idea, or fix a bug in complete isolation — without ever risking your stable, working code on `main`. When you're done, you bring the work back. If it doesn't work out, you just delete the branch and nothing is affected.

Every professional Git workflow — no matter the team size — is built around branches. Getting comfortable with them now will pay off for the rest of your career.

---

## Watch First

These videos will help you visualize how branches work before you start using them. The first one is especially good for building a mental model.

- **Git Branches Tutorial** (freeCodeCamp, 30min)
  https://www.youtube.com/watch?v=e2IbNHi4uCI

- **Git Branching and Merging** (The Net Ninja, 9min)
  https://www.youtube.com/watch?v=FyAAIHHClqI


---

## How Branches Work

When you create a branch, Git doesn't copy your entire project. It simply creates a new **pointer** — a lightweight label that points to the current commit. From that moment on, commits you make on the new branch move that pointer forward, while `main` stays exactly where it was.

```
main:       A ── B
                  \
feature/x:         C ── D
```

- `A` and `B` are commits on `main`
- You created `feature/x` at commit `B`
- Commits `C` and `D` exist only on `feature/x`
- `main` is completely unaware of `C` and `D` — until you merge

This isolation is the whole point. You can have multiple branches in flight at the same time, each representing a different piece of work, and they never interfere with each other.

Under the hood, a branch is just a file in `.git/refs/heads/` containing a 40-character commit hash. That's it. Creating a branch is nearly instant and costs almost nothing.

---

## Commands

```bash
# Viewing branches
git branch                          # list all local branches (* marks your current branch)
git branch -a                       # list local AND remote-tracking branches
git branch -v                       # list branches with their latest commit message

# Creating branches
git branch feature/login            # create a new branch (you stay on your current branch)
git checkout -b feature/login       # create a new branch AND switch to it immediately
git switch -c feature/login         # same as above, modern syntax (Git 2.23+)

# Switching between branches
git checkout feature/login          # switch to an existing branch
git switch feature/login            # modern way to switch (cleaner, less ambiguous)

# Renaming a branch
git branch -m old-name new-name     # rename a branch

# Deleting branches
git branch -d feature/login         # safe delete — Git refuses if the branch isn't merged yet
git branch -D feature/login         # force delete — removes it regardless of merge status

# Working with remotes
git push origin feature/login           # push your branch to the remote so others can see it
git push -u origin feature/login        # push and set upstream tracking
git push origin --delete feature/login  # delete the branch from the remote
```

---

## Understanding HEAD

You'll see `HEAD` mentioned everywhere in Git. It's simply a pointer to the commit you're currently on — usually the tip of your current branch.

```
HEAD --> main --> commit B
```

When you switch branches, HEAD moves:

```
HEAD --> feature/x --> commit D
```

When you run `git log`, the commit marked `(HEAD -> feature/x)` is where you are right now.

---

## Branch Naming Conventions

Good branch names make a repo much easier to navigate, especially on a team. The widely adopted convention uses a prefix that describes the type of work:

| Prefix | Purpose | Example |
|--------|---------|---------|
| `feature/` | New functionality | `feature/user-authentication` |
| `fix/` | Bug fixes | `fix/login-redirect-loop` |
| `hotfix/` | Urgent production fixes | `hotfix/payment-crash` |
| `chore/` | Maintenance, refactoring | `chore/update-dependencies` |
| `docs/` | Documentation only | `docs/api-reference` |

Keep names lowercase, use hyphens instead of spaces, and be specific enough that someone else knows what the branch is for without asking.

---

## Tasks

Work through these in order. Each one builds on the last.

- [ ] Create a new repo: `git init branch-practice && cd branch-practice`
- [ ] Create `index.txt`, write a line of text, stage it, and commit it on `main`
- [ ] Create a new branch called `feature/about` using `git checkout -b feature/about`
- [ ] Create `about.txt` on this branch, write some content, and commit it
- [ ] Switch back to `main` with `git switch main` — notice that `about.txt` is gone (it's safe on the other branch!)
- [ ] Run `git log --oneline --graph --all` — you should see both branches diverging from the same commit
- [ ] Create a second branch `feature/contact` from `main`, add `contact.txt`, and commit it
- [ ] Run `git log --oneline --graph --all` again — now you have three branches
- [ ] Delete `feature/about` with `git branch -d feature/about`
- [ ] Try to delete `feature/contact` with `git branch -d` — Git should warn you it's not merged yet
- [ ] Force delete it with `git branch -D feature/contact`

---

## Good to Know

- **Branches are cheap** — creating a branch takes milliseconds and uses almost no disk space. There's no reason to hesitate. Branch early and branch often.
- **`git branch` with no args** — the `*` marks your current branch. This is a quick sanity check when you're not sure where you are.
- **Deleting a branch is safe** — it only removes the pointer (label). The actual commits stay in Git's object store until garbage collection runs. If you accidentally delete a branch, you can often recover it with `git reflog`.
- **`git switch` vs `git checkout`** — `git checkout` is the older command that does many things (switch branches, restore files, etc.). `git switch` was introduced in Git 2.23 specifically for switching branches — it's clearer and harder to misuse. Both work; `git switch` is the modern preference.
- **You can't switch branches with uncommitted changes** — if you have unsaved work and try to switch, Git will either refuse or carry your changes over (depending on whether they conflict). Use `git stash` to temporarily save your work before switching.

---

## Lesson Complete?

Before moving on, make sure you can answer these:

1. What does `git checkout -b feature/x` do in one step?
2. Why does `about.txt` disappear when you switch back to `main`?
3. What's the difference between `git branch -d` and `git branch -D`?
4. What is `HEAD` and what does it point to?

When you're confident — head to **[Lesson 2: Merging -->](lesson-2.md)**
