# ArmaGit - Your Gateway to Git Mastery
Welcome to [ArmaGit](https://github.com/Armaritto/ArmaGit) , your ultimate Git guide! Whether you're a beginner or a pro, find everything you need to know about Git commands. Dive into the cheat sheets, tips, and tutorials to master version control, collaborate efficiently, and manage projects effectively. Let's unlock the secrets to seamless Git mastery together! <br>
Thanks [learngitbranching.js](https://learngitbranching.js.org/), my understanding of Git has significantly improved.

## Git Commits
- ### Git Add 
Used in Git to stage changes for commit. When you make modifications to files in your working directory, `git add` allows you to selectively choose which changes to include in the next commit. 
```
git add [file.extenstion]
```
To stage all changes in the current directory
```
git add .
```
- ### Git Commit 
Records a snapshot of all the (tracked) files in your directory. It's like a giant copy and paste.
```
git commit -m "[your_commit_message]"
```
To combine `git add` and `git commit` in a single command, you can use the `-a` flag with git commit. However, this command won't stage new files that haven't been previously tracked by Git.
```
git commit -a -m "[your_commit_message]"
```
- ### Git Log 
To view a history of commits in your repository and see the details of each commit, including the commit message, author, timestamp, and the changes made.
```
git log
```
To show the commits on branch1 and not in branch2
```
git log branch2..branch1
```
To show the commits that changed a file, even across renames
```
git log --follow [file.extension]
```
- ### Git Diff
Display the differences of what is changed but not staged
```
git diff
```
Display the differences of what is staged but not yet commited
```
git diff --staged
```
Display the differences of what is in branch1 and not in branch2
```
git diff branch2..branch1
```
- ### Detaching HEAD
`HEAD` is the symbolic name for the currently checked out commit -- it's essentially what commit you're working on top of. <br>
`Detaching HEAD` refers to when the HEAD reference in a Git repository points directly to a commit hash instead of pointing to a branch name. <br>
```
git checkout [commit_hash]
```
you'll end up in a detached HEAD state because you're directly checking out a specific commit.
```
git checkout [branch_name]
```
you'll be on the branch and HEAD will point to the branch reference. <br><br>
In summary, detaching HEAD is a temporary state that allows you to inspect and work with a specific commit directly. However, it's important to switch back to a branch or create a new branch if you intend to make further changes to avoid losing your work.
- ### Git Stash
Temporarily store modified files in order to change branches
```
git stash
```
List stack-ordered of stashed file changes
```
git stash list
```
Write working from the top of the stash stack
```
git stash pop
```
Discard the changes from the top of the stack list
```
git stash drop
```
- ### Git Status
Staged in Git refers to the state of changes that have been marked for inclusion in the next commit, allowing for selective preparation and organization of commit snapshots.
Staged changes will appear under the "Changes to be committed" section after running:
```
git status
```
- ### Git Reset
To Clear staged area and rewrite working tree from a specified commit we use
```
git reset --hard [commit]
```
## Git Branches
- ### Git Create Branches 
Allow you to work on multiple versions of your project simultaneously, keeping changes isolated until they're ready to be merged.
```
git branch [branch name]
```
- ### Git Checkout 
Lets you switch between different branches or revert files to previous states within your repository effortlessly.
```
git checkout [branch name]
```
To make a new branch and checkout on it in one shortcut you can use
```
git checkout -b [branch name]
```
<!-- To change the pointer of a branch and make it point to another one, you can use
```
git branch -f [branch-1] [branch-2]
```
-->
- ### Git Merge 
A command used in Git to integrate changes from one branch into another. It combines the changes made in a source branch with the target branch, creating a new merge commit if necessary.
```
git merge [branch name]
```  
- ### Git Rebase 
Rebasing essentially takes a set of commits, copies them, and plops them down somewhere else. It allows you to rewrite the commit history of your branch by moving, combining, or altering commits, providing a cleaner and more linear history for your project.
```
git rebase [branch name]
```
#### Merge vs Rebase
`git merge` preserves the original branching structure, while `git rebase` creates a cleaner, linear history by rewriting commit history. The choice between the two depends on the project's collaboration workflow and the desired commit history structure.

## Relative Refs
Shortcuts or references that allow you to identify commits relative to their current position in the commit history. They provide a convenient way to specify commits without needing to know or remember their full commit hashes.
- ### Caret `^` Operator
  Moving upwards one commit at a time with `^`
  ```
  git checkout main^
  ```
- ### Tilde `~` Notation
  Moving upwards a number of times with `~`
  ```
  git checkout HEAD~3
  ```
## Git Remote
- ### Git Clone
A command to create a copy of an existing Git repository on your local machine.
```
git clone [URL]
```
- ### Git Fetch
Downloads new data from the remote repository but does not integrate it into your working branch. It updates your local copy of remote branches, tags, and commits, allowing you to see what changes have occurred in the remote repository.
```
git fetch
```
- ### Git Pull
Integrates new data into your current working branch.
```
git pull [remote_name] [branch_name]
```
While there is a shortcut to `pull` from the current repository `origin` and merge in the `current branch`
```
git pull
```
### Fetch vs Pull
`git pull` is essentially a combination of `git fetch` followed by `git merge`. <br>
`git fetch` when you want to see what changes have been made in the remote repository without integrating them into your local branch immediately. It's useful for reviewing changes before merging or rebasing. <br>
`git pull` when you want to fetch changes from the remote repository and automatically merge them into your current working branch. It's convenient for quickly updating your local branch with changes from the remote repository.
<br><br>
### Stay tuned for updates! Coming soon.
