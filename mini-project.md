# Mini Project: Blog Site 📝

Apply everything from lessons 1–4 in a realistic workflow. You're building a simple blog site with multiple contributors (simulated by branches).

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

## Stage 1 — Feature Branches (Lesson 1 & 2)

### Task 1: About Page
- [ ] Create branch `feature/about-page`
- [ ] Add `about.html` with some content
- [ ] Commit: `feat: add about page`
- [ ] Merge into `main` (fast-forward)
- [ ] Delete the branch

### Task 2: First Blog Post
- [ ] Make a new commit on `main` first (add a `<nav>` to `index.html`)
- [ ] Create branch `feature/post-1`
- [ ] Add `post-1.html` with a title and body
- [ ] Commit: `feat: add first blog post`
- [ ] Merge into `main` — this will be a **3-way merge**
- [ ] Delete the branch

---

## Stage 2 — Conflict Resolution (Lesson 3)

### Task 3: Style Conflict
- [ ] On `main`, add to `index.html`: `<link rel="stylesheet" href="style.css">`
- [ ] Commit: `style: link stylesheet`
- [ ] Create branch `feature/dark-mode`
- [ ] On `feature/dark-mode`, change that same line to: `<link rel="stylesheet" href="dark.css">`
- [ ] Commit: `feat: use dark mode stylesheet`
- [ ] Switch to `main`, change the line to: `<link rel="stylesheet" href="main.css">`
- [ ] Commit: `style: rename stylesheet`
- [ ] Merge `feature/dark-mode` into `main` — **conflict!**
- [ ] Resolve: keep `main.css` but add a comment `<!-- dark mode ready -->`
- [ ] Stage, commit, delete branch

---

## Stage 3 — Rebase (Lesson 4)

### Task 4: Footer Feature
- [ ] Create branch `feature/footer`
- [ ] Add a `<footer>` tag to `index.html`, commit: `feat: add footer`
- [ ] Switch to `main`, add a `<meta charset="UTF-8">` tag to `index.html`, commit: `chore: add charset meta`
- [ ] Switch back to `feature/footer`
- [ ] Run `git rebase main` — replay footer commit on top of latest main
- [ ] Switch to `main`, merge `feature/footer` — should be **fast-forward**
- [ ] Delete the branch

---

## Final Check

```bash
git log --oneline --graph --all
```

Your history should show:
- A clean linear section from the rebase
- A merge commit from the 3-way merge
- A merge commit from the conflict resolution

---

## ✅ Completion Checklist

- [ ] Stage 1 done — two features merged
- [ ] Stage 2 done — conflict triggered and resolved
- [ ] Stage 3 done — rebase used for clean history
- [ ] Final `git log` shows a meaningful, readable history
