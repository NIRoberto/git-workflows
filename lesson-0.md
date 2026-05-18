# Lesson 0: Git Fundamentals

Before you touch branches or merging, you need a solid grip on the basics. This lesson covers how Git thinks, how it tracks your work, and all the everyday commands you'll use constantly throughout this tutorial and in real projects.

If you've used Git a little before, this is a great refresher. If you're brand new — welcome, you're in the right place.

---

## How Git Works

Git tracks your project as a series of **snapshots**, not file differences. Every time you commit, Git takes a picture of all your files at that moment and stores it.

There are three places your work lives:

```
Working Directory --> Staging Area --> Repository (.git)
  (your files)         (git add)        (git commit)
```

- **Working Directory** — where you edit files normally
- **Staging Area (Index)** — a holding area where you prepare changes before committing
- **Repository** — the permanent history stored in the `.git` folder

A typical workflow looks like this:

```
1. Edit a file
2. git add <file>       --> moves it to staging
3. git commit -m "..."  --> saves it to history
```

---

## Setting Up Git

Before anything else, tell Git who you are. This info gets attached to every commit you make.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

git config --global core.editor "code --wait"   # set VS Code as default editor
git config --list                                # verify your config
```

---

## Starting a Repository

```bash
git init                        # create a new repo in the current folder
git init my-project             # create a new repo in a new folder
git clone <url>                 # copy an existing remote repo locally
git clone <url> my-folder       # clone into a specific folder name
```

---

## Checking Status & History

These are the commands you'll run most often. Get comfortable with them.

```bash
git status                          # see what's changed, staged, or untracked
git log                             # full commit history
git log --oneline                   # compact one-line history
git log --oneline --graph --all     # visual history with branches
git diff                            # changes in working directory (not yet staged)
git diff --staged                   # changes that are staged (ready to commit)
git show <commit>                   # see what a specific commit changed
```

---

## Staging & Committing

```bash
git add <file>                  # stage a specific file
git add .                       # stage everything in the current directory
git add -p                      # interactively stage chunks of changes

git commit -m "your message"    # commit with an inline message
git commit                      # opens editor to write a longer message
git commit --amend              # edit the last commit message (before pushing)
```

> Note: Write commit messages in the imperative — "add login page", not "added login page". It reads like a changelog and is the widely accepted convention.

---

## Undoing Things

This is where a lot of people get nervous. Here's a clear breakdown:

```bash
# Unstage a file (keep changes in working directory)
git restore --staged <file>

# Discard changes in working directory (permanent — be careful)
git restore <file>

# Undo the last commit but keep the changes staged
git reset --soft HEAD~1

# Undo the last commit and unstage the changes
git reset --mixed HEAD~1

# Undo the last commit and throw away the changes (permanent)
git reset --hard HEAD~1

# Safely undo a commit by creating a new "reverse" commit
git revert <commit>
```

> Note: Use `git revert` on shared branches. Use `git reset` only on your own local commits that haven't been pushed.

---

## Working with Remote Repositories

```bash
git remote -v                           # list connected remotes
git remote add origin <url>             # connect a remote called "origin"

git fetch                               # download changes without merging
git pull                                # fetch + merge into current branch
git pull --rebase                       # fetch + rebase instead of merge

git push origin main                    # push local main to remote
git push -u origin main                 # push and set upstream (first time)
git push                                # push to tracked upstream (after -u is set)
```

---

## Stashing Work

Stash lets you temporarily save uncommitted work so you can switch context without losing anything.

```bash
git stash                       # stash current changes
git stash push -m "wip: login"  # stash with a descriptive name
git stash list                  # see all stashes
git stash pop                   # apply the latest stash and remove it
git stash apply stash@{1}       # apply a specific stash (keep it in the list)
git stash drop stash@{1}        # delete a specific stash
git stash clear                 # delete all stashes
```

---

## Viewing & Comparing

```bash
git log --author="Name"             # filter commits by author
git log --since="2 weeks ago"       # filter commits by date
git log --grep="fix"                # filter commits by message keyword
git log <file>                      # history of a specific file

git diff main..feature/x            # compare two branches
git diff HEAD~3                     # compare current state to 3 commits ago
```

---

## Ignoring Files

Create a `.gitignore` file in your repo root to tell Git what to ignore.

```
# .gitignore examples
node_modules/
.env
*.log
dist/
.DS_Store
```

```bash
git check-ignore -v <file>      # find out why a file is being ignored
```

---

## Tasks

- [ ] Install Git and run `git --version` to confirm it's working
- [ ] Set your `user.name` and `user.email` with `git config --global`
- [ ] Create a new repo with `git init fundamentals-practice`
- [ ] Create a file, stage it with `git add`, and commit it with a message
- [ ] Edit the file, use `git diff` to see the change, then stage and commit again
- [ ] Run `git log --oneline` to see your two commits
- [ ] Make a change, then use `git restore <file>` to discard it
- [ ] Make another change, stage it, then use `git restore --staged <file>` to unstage it
- [ ] Create a `.gitignore` file and add `*.log` to it, then create a `test.log` file and confirm Git ignores it

---

## Good to Know

- **`git status` is your best friend** — run it constantly. It always tells you exactly what state you're in.
- **Commits are permanent (mostly)** — once committed, your work is safe. You can always get back to any commit.
- **The staging area is intentional** — it lets you craft clean, focused commits even when you've changed many files at once.
- **`.git` folder = your entire history** — never delete it. Everything Git knows about your project lives there.

---

## Lesson Complete?

Before moving on, make sure you can answer these:

1. What are the three areas where your work lives in Git?
2. What is the difference between `git fetch` and `git pull`?
3. When would you use `git revert` instead of `git reset`?

Ready to start branching? Head to **[Lesson 1: Branches -->](lesson-1.md)**
