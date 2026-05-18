# Mini Project: Blog Site

You've made it to the mini project — this is where everything comes together. You're going to build a simple blog site using Git the way a real developer would. Each task maps directly to one of the four lessons, so you'll use every concept you've learned in a realistic scenario.

Don't rush. Read each task fully before you start. The goal isn't just to check boxes — it's to understand why you're doing each step.

---

## Watch First

These videos show real-world Git workflows in action — great context before you start.

- **Git and GitHub Full Course for Beginners** (freeCodeCamp, 1hr)
  https://www.youtube.com/watch?v=RGOj5yH7evk

- **Git for Professionals — Full Course** (freeCodeCamp, 40min)
  https://www.youtube.com/watch?v=Uszj_k0DGsg

- **A Practical Git Workflow** (Traversy Media, 20min)
  https://www.youtube.com/watch?v=DVRQoVRzMIY

---

## What You're Building

A simple static blog site. The content is up to you — what matters is the Git workflow you use to build it.

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

Create a new folder called `blog-site`, initialize a Git repo inside it, and create a basic `index.html` homepage with a title and a welcome message. Add a `.gitignore` that ignores log files and OS-specific files. Stage everything and make your first commit on `main` with a clear message.

This is your starting point. Everything from here is built on top of this commit.

---

## Task 1 — Add the About Page (Lesson 1: Branches)

**Concept:** Creating a branch, doing work on it, and keeping it isolated from `main`.

You've been asked to add an about page to the blog. Create a feature branch for this work — don't touch `main` directly. On the branch, create `about.html` with a heading and a short description of what the blog is about. Make a focused, well-named commit. When you're done, switch back to `main` and confirm that `about.html` is not there — it only exists on your branch.

Don't merge yet. Just get comfortable with the idea that your work is safely isolated on its own branch while `main` stays untouched.

**What to confirm before moving on:**
- [ ] The branch exists and has at least one commit
- [ ] `about.html` is NOT visible when you switch back to `main`
- [ ] `git log --oneline --graph --all` shows both branches

---

## Task 2 — Add the Navigation Bar (Lesson 2: Merging)

**Concept:** Merging branches — both fast-forward and three-way.

Now it's time to bring your work back. First, merge the `feature/about-page` branch into `main`. Since `main` hasn't changed, this should be a clean fast-forward — confirm that in the output.

Next, simulate a three-way merge. Make a new commit directly on `main` (add a `README.md` with a short project description). Then create a new branch `feature/navigation`, add a nav bar to `index.html` that links to the about page, and commit it. When you merge this branch back into `main`, both branches have diverged — Git will create a merge commit. Write a clear merge commit message and confirm the branching shape in `git log --oneline --graph`.

Delete both feature branches after merging.

**What to confirm before moving on:**
- [ ] First merge was a fast-forward (no merge commit)
- [ ] Second merge created a merge commit with two parents
- [ ] `git log --oneline --graph` shows the branching and merge shape
- [ ] Both feature branches are deleted

---

## Task 3 — Add Blog Posts and Resolve a Conflict (Lesson 3: Merge Conflicts)

**Concept:** Triggering a real merge conflict and resolving it properly.

Create a branch `feature/post-1` and add `post-1.html` — a blog post about anything you like. Make two separate, focused commits on this branch: one for creating the post file, and one for linking it from `index.html`. Merge it into `main`.

Now simulate a conflict. On `main`, change the blog's title in `index.html` to one name. Create a branch `feature/post-2`, change the same title to a different name, and also add `post-2.html` with a second blog post. Switch back to `main` and merge `feature/post-2`. You'll get a conflict on the title line.

Resolve the conflict by choosing the final title you want, removing all conflict markers, staging the file, and completing the merge. Run `git log --oneline --graph` to confirm the merge commit.

**What to confirm before moving on:**
- [ ] Two focused commits on `feature/post-1` (one for the file, one for the link)
- [ ] Conflict was triggered on the title line
- [ ] Conflict markers are fully removed before committing
- [ ] Merge commit is visible in `git log --oneline --graph`

---

## Task 4 — Add Stylesheet and Clean Up History (Lesson 4: Rebase)

**Concept:** Rebasing a feature branch onto `main` for a clean fast-forward, and using interactive rebase to squash messy commits.

Create a branch `feature/styles` and start adding `style.css`. Make several small, messy commits as you work — things like "wip: start styles", "fix: adjust font", "wip: more styles". This is realistic — developers often commit frequently while experimenting.

Before merging, use `git rebase -i` to squash all those messy commits into a single clean commit with a proper message like `feat: add base stylesheet`. This is what you'd do before opening a pull request on a real team.

Now simulate the rebase workflow. Make a new commit on `main` (update the README with a list of posts). Switch back to `feature/styles` and rebase it onto `main` so your branch sits on top of the latest commit. Switch to `main` and merge — it should be a clean fast-forward with no merge commit.

Delete the branch and run `git log --oneline --graph --all` to review your complete history.

**What to confirm before moving on:**
- [ ] Messy commits were squashed into one clean commit using `git rebase -i`
- [ ] Rebase onto `main` was successful
- [ ] Final merge was a fast-forward (no merge commit)
- [ ] `git log --oneline --graph --all` shows a clean, readable history

---

## Final History Check

After all four tasks, run:

```bash
git log --oneline --graph --all
```

Your history should show:
- A fast-forward merge from Task 1
- A three-way merge commit from Task 2
- A conflict resolution merge commit from Task 3
- A clean linear section from the rebase in Task 4

If it looks like that — you've done it. That's a real, professional Git history built the right way.

---

## Completion Checklist

- [ ] Task 1 — about page on its own branch, isolated from `main`
- [ ] Task 2 — fast-forward merge and three-way merge both completed
- [ ] Task 3 — conflict triggered, resolved cleanly, merge commit confirmed
- [ ] Task 4 — messy commits squashed, rebase used, fast-forward merge confirmed
- [ ] Final `git log --oneline --graph` tells the full story of the project
