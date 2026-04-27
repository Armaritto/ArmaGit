# ArmaGit — Git Mastery Reference

> A comprehensive Git command reference for developers at every level. From first commits to remote workflows, everything you need in one place. <br>
Thanks [learngitbranching.js](https://learngitbranching.js.org/), my understanding of Git has significantly improved.

---

## Table of Contents

- [Working with Commits](#working-with-commits)
- [Branching](#branching)
- [Relative References](#relative-references)
- [Remote Repositories](#remote-repositories)
- [Origins & Remote Branches](#origins--remote-branches)
- [Debugging with Bisect](#debugging-with-bisect)

---

## Working with Commits

### Staging Changes — `git add`

Selectively stage changes from your working directory for the next commit.

```bash
# Stage a specific file
git add <file.ext>

# Stage all changes in the current directory
git add .
```

---

### Recording Changes — `git commit`

Saves a snapshot of all staged (tracked) files in your repository.

```bash
# Commit with a message
git commit -m "<your commit message>"

# Stage all tracked files and commit in one step
# Note: does not include new, untracked files
git commit -a -m "<your commit message>"
```

---

### Viewing History — `git log`

Inspect the commit history of your repository.

```bash
# Full commit history
git log

# Show commits in branch1 that are not in branch2
git log branch2..branch1

# Show commits that modified a specific file (follows renames)
git log --follow -- <file.ext>
```

---

### Comparing Changes — `git diff`

Examine differences between states of your repository.

```bash
# Changes not yet staged
git diff

# Changes staged but not yet committed
git diff --staged

# Changes in branch1 not present in branch2
git diff branch2..branch1
```

---

### Stashing Work — `git stash`

Temporarily shelve uncommitted changes so you can switch context.

```bash
# Stash current changes
git stash

# List all stashed entries
git stash list

# Restore the most recent stash
git stash pop

# Discard the most recent stash
git stash drop
```

---

### Checking State — `git status`

Shows the state of your working directory and staging area.

```bash
git status
```

Staged changes appear under **"Changes to be committed"**. Staging lets you selectively build commits from your working changes.

---

### Undoing Changes — `git reset`

Resets the staging area and rewrites the working tree to match a specific commit.

```bash
git reset --hard <commit>
```

> ⚠️ **Warning:** `--hard` is destructive. Any uncommitted changes will be permanently lost.

---

### Detaching HEAD

`HEAD` is the symbolic pointer to your currently checked-out commit. When you check out a commit directly (rather than a branch), HEAD enters a **detached** state.

```bash
# Detach HEAD to a specific commit
git checkout <commit-hash>

# Re-attach HEAD to a branch
git checkout <branch-name>
```

> Detached HEAD is useful for inspecting history, but avoid making new commits in this state without first creating a branch — your work may otherwise be unreachable.

---

### Cherry-Picking — `git cherry-pick`

Apply specific commits from one branch onto another, without merging entire branches.

```bash
git cherry-pick <commit-hash-1> <commit-hash-2> ...
```

---

## Branching

### Creating Branches

Branches let you work on isolated features or fixes in parallel.

```bash
git branch <branch-name>
```

---

### Switching Branches — `git checkout`

Move between branches or restore files to a previous state.

```bash
# Switch to an existing branch
git checkout <branch-name>

# Create a new branch and switch to it immediately
git checkout -b <branch-name>
```

---

### Merging — `git merge`

Integrate changes from one branch into another. Creates a merge commit when the histories have diverged.

```bash
git merge <branch-name>
```

---

### Rebasing — `git rebase`

Replay commits from your branch on top of another, producing a clean, linear history.

```bash
git rebase <branch-name>
```

---

### Merge vs. Rebase

| | `git merge` | `git rebase` |
|---|---|---|
| **History** | Preserves branching structure | Rewrites to a linear history |
| **Commit graph** | Non-linear, shows true history | Linear, easier to read |
| **Best for** | Public/shared branches | Local feature cleanup |

**Typical workflow when remote has diverged:**

```bash
# With rebase (cleaner history)
git pull --rebase
git push

# With merge (safer for shared branches)
git pull
git push
```

---

## Relative References

Relative refs let you navigate commit history without needing full commit hashes.

### Caret `^` — Move Up One Commit

```bash
git checkout main^
```

### Tilde `~` — Move Up N Commits

```bash
git checkout HEAD~3
```

---

## Remote Repositories

### Cloning — `git clone`

Create a local copy of a remote repository.

```bash
git clone <URL>
```

---

### Fetching — `git fetch`

Download changes from the remote without integrating them into your working branch.

```bash
git fetch
```

---

### Pulling — `git pull`

Fetch and immediately merge remote changes into your current branch.

```bash
# Full form
git pull <remote-name> <branch-name>

# Shorthand — pulls from origin into current branch
git pull
```

---

### Fetch vs. Pull

| | `git fetch` | `git pull` |
|---|---|---|
| **What it does** | Downloads remote changes | Fetch + merge |
| **Working branch** | Unchanged | Updated immediately |
| **Best for** | Reviewing before integrating | Quickly syncing your branch |

`git pull` is equivalent to running `git fetch` followed by `git merge`.

---

### Handling Push Rejection on Protected Branches

On collaborative projects, pushing directly to `main` is often blocked by policy:

```
! [remote rejected] main -> main (TF402455: Pushes to this branch are not permitted; you must use a pull request to update this branch.)
```

**If you have write access, use a feature branch:**

```bash
git checkout -b feature
git add .
git commit -m "Implement feature"
git push origin feature

# Reset local main to match remote
git checkout main
git fetch origin
git reset --hard origin/main
```

**If you don't have write access:**

1. Fork the repository to your own GitHub account.
2. Follow the steps above in your fork.
3. Open a pull request to contribute back to the original repository.

---

## Origins & Remote Branches

`origin` is the default alias for the remote repository your local repo was cloned from.

`origin/main` is a **remote-tracking branch** — a local read-only snapshot of the remote's `main` as of your last communication with it. It helps you understand how your local work differs from what's published.

> Checking out a remote branch puts you in detached HEAD mode by design. You cannot commit to remote branches directly; changes must go through your local branches and then be pushed.

```bash
# Inspect a remote branch (puts you in detached HEAD)
git checkout origin/main
git commit
# origin/main does NOT move — it only updates when you fetch/pull
```

---

## Debugging with Bisect

Use binary search to efficiently locate the commit that introduced a bug.

```bash
# Start a bisect session
git bisect start
git bisect bad                  # Mark current commit as broken
git bisect good v2.6.13-rc2     # Mark a known-good commit or tag
```

Git checks out a midpoint commit. Test it, then mark it:

```bash
git bisect good   # This commit works
git bisect bad    # This commit is broken
```

Repeat until Git identifies the first bad commit. Then clean up:

```bash
git bisect reset
```

> Bisect uses binary search, so it finds the culprit in **O(log n)** steps — typically around 10 steps even across hundreds of commits.


*This reference is actively maintained. New commands and concepts are added as they're encountered.*
