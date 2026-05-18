# Lesson 4: Rebase 🔁

Rebase rewrites your branch's commits on top of another branch, giving you a **clean, linear history** — no merge commits.

---

## Merge vs Rebase

```
# After merge:
main:    A --- B --- E --- M
                \         /
feature:         C --- D

# After rebase:
main:    A --- B --- E --- C' --- D'
```

Rebase replays `C` and `D` as if they were written after `E`. The commits get new hashes (`C'`, `D'`).

---

## Commands

```bash
git checkout feature/x
git rebase main               # replay feature commits on top of main

git rebase --continue         # after resolving a conflict mid-rebase
git rebase --abort            # cancel and go back to original state
git rebase --skip             # skip a commit that causes a conflict

git log --oneline --graph     # verify clean linear history
```

---

## Rebase Conflict Flow

Conflicts during rebase are resolved **per commit**, not all at once:

1. Rebase pauses at the conflicting commit
2. Fix the conflict in the file
3. `git add <file>`
4. `git rebase --continue` — moves to the next commit
5. Repeat until done

---

## ✅ Tasks

- [ ] Create a repo, make 2 commits on `main` (`A`, `B`)
- [ ] Create `feature/rebase-test`, make 2 commits (`C`, `D`)
- [ ] Switch back to `main`, make 1 more commit (`E`)
- [ ] Switch to `feature/rebase-test`, run `git rebase main`
- [ ] Run `git log --oneline --graph` — history should be linear
- [ ] Merge `feature/rebase-test` into `main` — it should fast-forward

---

## ✅ Bonus — Rebase with Conflict

- [ ] On `main` and `feature/rebase-test`, edit the **same line** in the same file
- [ ] Run `git rebase main` from the feature branch
- [ ] Resolve the conflict, `git add`, then `git rebase --continue`
- [ ] Confirm clean history after

---

## ⚠️ Golden Rule

> Never rebase a branch that others are working on.

Rebase rewrites commit hashes. If someone else has those commits, their history will diverge and cause chaos. Only rebase **your own local branches**.

---

## 💡 Merge vs Rebase — When to Use

| Situation | Use |
|-----------|-----|
| Shared/public branch | Merge |
| Local feature branch cleanup | Rebase |
| Want to preserve full history | Merge |
| Want clean linear history | Rebase |
