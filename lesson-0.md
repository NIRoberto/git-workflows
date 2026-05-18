# Lesson 0: Git Fundamentals

Before you touch branches or merging, you need a solid grip on the basics. This lesson covers how Git thinks, how it tracks your work, and all the everyday commands you'll use constantly — not just in this tutorial, but in every real project you'll ever work on.

If you've used Git a little before, this is a great refresher. If you're brand new — welcome, you're in exactly the right place. Take your time here. Everything in the later lessons depends on what you learn in this one.

---

## Watch First

These videos will give you a strong visual foundation before you start running commands. Watch them in order — they complement each other well.

- **Git and GitHub for Beginners — Crash Course** (freeCodeCamp, 1hr)
  https://www.youtube.com/watch?v=RGOj5yH7evk

- **Git Tutorial for Beginners: Learn Git in 1 Hour** (Programming with Mosh, 1hr)
  https://www.youtube.com/watch?v=8JJ101D3knE

- **Git Explained in 100 Seconds** (Fireship, quick overview)
  https://www.youtube.com/watch?v=hwP7WQkmECE

---

## How Git Works

Most version control systems track changes as a list of file differences (what changed on line X). Git works differently — it tracks your project as a series of **snapshots**. Every time you commit, Git takes a complete picture of all your files at that exact moment and stores a reference to it. If a file hasn't changed, Git doesn't store it again — it just links to the previous version.

This snapshot model is what makes Git so fast and reliable. You're not dealing with patches — you're dealing with full states of your project at specific points in time.

There are three places your work lives at any given moment:

```
Working Directory --> Staging Area --> Repository (.git)
  (your files)         (git add)        (git commit)
```

- **Working Directory** — this is your normal file system. When you open a file and edit it, you're working here. Git sees these changes but hasn't recorded them yet.

- **Staging Area (also called the Index)** — a preparation zone. You explicitly move changes here with `git add`. This lets you choose exactly what goes into your next commit, even if you've changed many files.

- **Repository** — the permanent, compressed history of your project stored in the hidden `.git` folder. Once something is committed here, it's safe and retrievable.

A typical day-to-day workflow looks like this:

```
1. Edit a file in your working directory
2. git add <file>        --> promotes it to the staging area
3. git commit -m "..."   --> saves the staged snapshot to history
```

Understanding this three-step flow is the single most important thing in this lesson. Everything else builds on it.

---

## Setting Up Git

Before you make your first commit, you need to tell Git who you are. This information gets permanently attached to every commit you make — it's how teams know who did what.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

git config --global core.editor "code --wait"   # use VS Code as your editor
git config --global init.defaultBranch main      # name the default branch "main"
git config --list                                # verify everything looks right
```

The `--global` flag means these settings apply to all repos on your machine. You can override them per-repo by running the same commands without `--global` inside a specific project folder.

---

## Starting a Repository

There are two ways to get a Git repo: create one from scratch, or clone an existing one.

```bash
# Starting fresh
git init                        # turn the current folder into a Git repo
git init my-project             # create a new folder and initialize it as a repo

# Cloning an existing repo
git clone <url>                 # download a remote repo into a new folder
git clone <url> my-folder       # same, but name the folder yourself
```

When you run `git init`, Git creates a hidden `.git` folder. That folder IS your repository — it contains your entire history, configuration, and everything Git needs. Never delete it manually.

When you `git clone`, you get a full copy of the repo including all history, all branches, and a remote connection called `origin` already set up for you.

---

## Checking Status & History

These are the commands you'll run most often. Make them second nature.

```bash
git status                          # the most important command — shows exactly what's going on
git log                             # full commit history with author, date, and message
git log --oneline                   # compact one-line-per-commit view
git log --oneline --graph --all     # visual ASCII graph of all branches and commits
git diff                            # shows changes in your working directory not yet staged
git diff --staged                   # shows changes that ARE staged, ready to commit
git show <commit>                   # shows the full diff of a specific commit
```

`git status` deserves special mention. Run it before and after every command when you're learning. It tells you which files are modified, which are staged, which are untracked, and what you should do next. It's like a GPS for your repo.

---

## Staging & Committing

```bash
git add <file>                  # stage a specific file
git add .                       # stage all changes in the current directory
git add -p                      # interactively choose which chunks to stage (very useful)

git commit -m "your message"    # commit with a short inline message
git commit                      # opens your editor for a longer, multi-line message
git commit --amend              # rewrite the last commit message or add forgotten changes
```

**Writing good commit messages matters.** A well-written history is a gift to your future self and your teammates. Follow these conventions:

- Use the imperative mood: `add login page`, not `added login page` or `adding login page`
- Keep the first line under 72 characters
- If more context is needed, leave a blank line and write a longer description below

Good: `fix: prevent crash when user has no profile photo`
Bad: `fixed stuff`

---

## Undoing Things

This is the section most people are afraid of. Don't be — Git almost never permanently deletes anything. Here's a clear map of your options:

```bash
# --- Before committing ---

# Unstage a file (changes stay in your working directory)
git restore --staged <file>

# Discard all changes to a file in your working directory (this IS permanent)
git restore <file>


# --- After committing ---

# Undo the last commit, keep changes staged and ready to re-commit
git reset --soft HEAD~1

# Undo the last commit, keep changes in working directory but unstaged
git reset --mixed HEAD~1

# Undo the last commit AND throw away all the changes (use with caution)
git reset --hard HEAD~1

# Create a new commit that reverses a previous commit (safe for shared branches)
git revert <commit-hash>
```

The key distinction: `git reset` rewrites history (dangerous on shared branches), while `git revert` adds a new commit that undoes the changes (safe anywhere). When in doubt, use `git revert`.

---

## Working with Remote Repositories

A remote is a version of your repo hosted somewhere else — usually GitHub, GitLab, or Bitbucket. This is how you back up your work and collaborate with others.

```bash
git remote -v                           # list all connected remotes and their URLs
git remote add origin <url>             # connect your local repo to a remote called "origin"

git fetch                               # download changes from remote but don't apply them yet
git fetch --all                         # fetch from all remotes

git pull                                # fetch + merge remote changes into your current branch
git pull --rebase                       # fetch + rebase instead of merge (cleaner history)

git push origin main                    # push your local main branch to the remote
git push -u origin main                 # push and set the upstream tracking (do this the first time)
git push                                # push to the tracked upstream (works after -u is set)
```

`git fetch` vs `git pull` is a common point of confusion. Think of it this way: `fetch` downloads the changes and lets you review them first. `pull` downloads and immediately applies them. When working on a team, `fetch` first is the safer habit.

---

## Stashing Work

Stash is a temporary shelf for work you're not ready to commit. It's incredibly useful when you need to switch branches quickly but have unfinished changes you don't want to lose or commit yet.

```bash
git stash                           # stash all current changes
git stash push -m "wip: login form" # stash with a descriptive label
git stash list                      # see all your stashes
git stash pop                       # apply the most recent stash and remove it from the list
git stash apply stash@{1}           # apply a specific stash but keep it in the list
git stash drop stash@{1}            # delete a specific stash
git stash clear                     # delete all stashes
```

A common scenario: you're halfway through a feature when a critical bug comes in. You `git stash` your work-in-progress, fix the bug on a new branch, then come back and `git stash pop` to pick up exactly where you left off.

---

## Viewing & Comparing

```bash
# Filtering the log
git log --author="Name"             # commits by a specific author
git log --since="2 weeks ago"       # commits from the last 2 weeks
git log --until="2024-01-01"        # commits before a specific date
git log --grep="fix"                # commits whose message contains "fix"
git log -- <file>                   # full history of a specific file

# Comparing
git diff main..feature/x            # what's different between two branches
git diff HEAD~3                     # compare current state to 3 commits ago
git diff <commit1> <commit2>        # compare any two commits
```

---

## Ignoring Files

Some files should never be committed — build artifacts, environment variables, editor configs, OS files. The `.gitignore` file tells Git to completely ignore them.

Create a `.gitignore` file in your repo root:

```
# Dependencies
node_modules/
vendor/

# Environment variables (never commit these)
.env
.env.local

# Build output
dist/
build/
*.log

# OS files
.DS_Store
Thumbs.db

# Editor configs
.vscode/
.idea/
```

```bash
git check-ignore -v <file>      # debug why a file is being ignored
```

> Important: If you accidentally committed a file before adding it to `.gitignore`, just adding it to `.gitignore` won't remove it from history. You'll need `git rm --cached <file>` to stop tracking it.

---

## Tasks

Work through all of these before moving on. They cover every concept in this lesson.

- [ ] Install Git and run `git --version` to confirm it's working
- [ ] Configure your name and email with `git config --global`
- [ ] Create a new repo: `git init fundamentals-practice && cd fundamentals-practice`
- [ ] Create `readme.txt`, write a couple of lines, stage it, and commit with a meaningful message
- [ ] Edit `readme.txt`, run `git diff` to see the change, then stage and commit again
- [ ] Run `git log --oneline` — you should see two commits
- [ ] Make another change, then use `git restore <file>` to discard it — confirm the change is gone
- [ ] Make a change, stage it, then use `git restore --staged <file>` to unstage it — confirm it's back in the working directory
- [ ] Make one more commit, then use `git reset --soft HEAD~1` to undo it — confirm the changes are still staged
- [ ] Create a `.gitignore`, add `*.log` to it, create `debug.log`, and confirm `git status` doesn't show it

---

## Good to Know

- **`git status` is your best friend** — run it constantly, especially when learning. It always tells you exactly what state you're in and what to do next.
- **Commits are (almost) permanent** — once committed, your work is safe. You can always get back to any commit using its hash. Very little in Git is truly irreversible.
- **The staging area is a feature, not a formality** — it lets you craft clean, focused commits even when you've changed many files at once. Use `git add -p` to stage only the relevant chunks.
- **The `.git` folder is your entire project history** — never delete it manually. If you want to "un-Git" a project, just delete the `.git` folder, but know that you'll lose all history.
- **Git is local-first** — almost every operation (commit, branch, log, diff) works completely offline. You only need a network connection for `push`, `pull`, and `fetch`.

---

## Lesson Complete?

Before moving on, make sure you can answer these:

1. What are the three areas where your work lives in Git, and what moves it between them?
2. What is the difference between `git fetch` and `git pull`?
3. When would you use `git revert` instead of `git reset`, and why?
4. What does `git add -p` do and why is it useful?

Take your time with this lesson — a strong foundation here makes everything else much easier. When you're ready, head to **[Lesson 1: Branches -->](lesson-1.md)**
