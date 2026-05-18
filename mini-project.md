# Mini Project: Blog Site

Build a simple blog site using Git. Each task covers one lesson. By the end you'll have a real Git history that shows branches, merges, conflict resolution, and rebase all in one project.

---

## Watch First

- **Git and GitHub Full Course for Beginners** (freeCodeCamp, 1hr)
  https://www.youtube.com/watch?v=RGOj5yH7evk

- **Git for Professionals** (freeCodeCamp, 40min)
  https://www.youtube.com/watch?v=Uszj_k0DGsg

- **A Practical Git Workflow** (Traversy Media, 20min)
  https://www.youtube.com/watch?v=DVRQoVRzMIY

---

## What You're Building

```
blog-site/
├── index.html      # homepage
├── about.html      # about page
├── post-1.html     # first blog post
├── post-2.html     # second blog post
├── style.css       # shared styles
└── .gitignore      # ignored files
```

---

## Setup

Create a `blog-site` folder, init a Git repo, add a basic `index.html` and a `.gitignore`. Make your first commit on `main`. That's your starting point.

---

## Task 1 — About Page (Lesson 1: Branches)

Create a branch `feature/about-page`. Add `about.html` and commit it. Switch back to `main` and confirm the file isn't there — it should only exist on the branch. Don't merge yet.

- [ ] Branch exists with at least one commit
- [ ] `about.html` is not visible on `main`
- [ ] `git log --oneline --graph --all` shows both branches

---

## Task 2 — Navigation Bar (Lesson 2: Merging)

Merge `feature/about-page` into `main` — it should fast-forward. Then make a new commit on `main` (add a `README.md`), create `feature/navigation`, add a nav bar to `index.html`, and merge it back. This time `main` has moved so Git creates a merge commit. Delete both branches after.

- [ ] First merge was a fast-forward
- [ ] Second merge created a merge commit
- [ ] `git log --oneline --graph` shows the branching shape
- [ ] Both branches deleted

---

## Task 3 — Blog Posts + Conflict (Lesson 3: Merge Conflicts)

Create `feature/post-1`, add `post-1.html`, and link it from `index.html` in two separate commits. Merge into `main`. Then on `main` change the blog title in `index.html`. Create `feature/post-2`, change the same title to something different, add `post-2.html`, and merge back. You'll get a conflict — resolve it, remove all markers, stage, and commit.

- [ ] Two focused commits on `feature/post-1`
- [ ] Conflict triggered on the title line
- [ ] All conflict markers removed before committing
- [ ] Merge commit visible in `git log --oneline --graph`

---

## Task 4 — Stylesheet + Rebase (Lesson 4: Rebase)

Create `feature/styles`, add `style.css` across several messy commits ("wip", "fix", etc.). Before merging, use `git rebase -i` to squash them into one clean commit. Then make a new commit on `main` (update the README). Rebase `feature/styles` onto `main` and merge — it should fast-forward cleanly.

- [ ] Messy commits squashed into one with `git rebase -i`
- [ ] Branch rebased onto latest `main`
- [ ] Final merge was a fast-forward
- [ ] `git log --oneline --graph --all` shows a clean history

---

## Final Check

```bash
git log --oneline --graph --all
```

You should see a fast-forward, a three-way merge commit, a conflict resolution commit, and a clean linear section from the rebase. If it does — you're done.

---

## Completion Checklist

- [ ] Task 1 — branch created, work isolated from `main`
- [ ] Task 2 — fast-forward and three-way merge done
- [ ] Task 3 — conflict resolved, merge commit confirmed
- [ ] Task 4 — commits squashed, rebase done, fast-forward confirmed
- [ ] Final `git log --oneline --graph` looks clean and readable
