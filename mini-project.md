# Mini Project: Blog Site

You've made it to the mini project — this is where everything comes together. You're going to build a simple blog site using a realistic Git workflow, covering branches, merging, conflict resolution, and rebase all in one go.

By the end of this, you'll have a clean Git history that tells the full story of how the project was built.

---

## Project Structure

```
blog-site/
├── index.html       # homepage
├── about.html       # about page
├── post-1.html      # first blog post
└── style.css        # shared styles
```

---

## Setup

```bash
mkdir blog-site && cd blog-site
git init
```

Create `index.html`:

```html
<h1>My Blog</h1>
<p>Welcome to my blog.</p>
```

```bash
git add . && git commit -m "init: add homepage"
```

---

## Stage 1 — Feature Branches (Lessons 1 & 2)

### Task 1: About Page

- [ ] Create branch `feature/about-page`
- [ ] Add `about.html` with some content
- [ ] Commit: `feat: add about page`
- [ ] Switch to `main` and merge — this should be a **fast-forward**
- [ ] Delete the branch

### Task 2: First Blog Post

- [ ] Make a new commit on `main` first — add a `<nav>` element to `index.html`, commit: `feat: add nav`
- [ ] Create branch `feature/post-1`
- [ ] Add `post-1.html` with a title and a short body
- [ ] Commit: `feat: add first blog post`
- [ ] Switch to `main` and merge — this will be a **3-way merge**
- [ ] Delete the branch

---

## Stage 2 — Conflict Resolution (Lesson 3)

### Task 3: Stylesheet Conflict

- [ ] On `main`, add this line to `index.html`: `<link rel="stylesheet" href="style.css">`
- [ ] Commit: `style: link stylesheet`
- [ ] Create branch `feature/dark-mode`
- [ ] On `feature/dark-mode`, change that line to: `<link rel="stylesheet" href="dark.css">`
- [ ] Commit: `feat: use dark mode stylesheet`
- [ ] Switch back to `main`, change the same line to: `<link rel="stylesheet" href="main.css">`
- [ ] Commit: `style: rename stylesheet`
- [ ] Merge `feature/dark-mode` into `main` — **conflict!**
- [ ] Resolve it: keep `main.css` and add a comment `<!-- dark mode ready -->`
- [ ] Stage, commit, and delete the branch

---

## Stage 3 — Rebase (Lesson 4)

### Task 4: Footer Feature

- [ ] Create branch `feature/footer`
- [ ] Add a `<footer>` element to `index.html`, commit: `feat: add footer`
- [ ] Switch to `main`, add `<meta charset="UTF-8">` to `index.html`, commit: `chore: add charset meta`
- [ ] Switch back to `feature/footer`
- [ ] Run `git rebase main` — replay the footer commit on top of the latest `main`
- [ ] Switch to `main` and merge `feature/footer` — should be a clean **fast-forward**
- [ ] Delete the branch

---

## Final Check

Run this to see your full history:

```bash
git log --oneline --graph --all
```

Your history should show:
- A clean linear section from the rebase in Stage 3
- A merge commit from the 3-way merge in Stage 1
- A merge commit from the conflict resolution in Stage 2

If it does — you nailed it.

---

## Completion Checklist

- [ ] Stage 1 complete — two feature branches created and merged
- [ ] Stage 2 complete — conflict triggered, resolved, and committed
- [ ] Stage 3 complete — rebase used for a clean linear history
- [ ] Final `git log --oneline --graph` shows a meaningful, readable history
