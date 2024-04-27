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
git log --follow -- [file.extension]
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
- ### Cherry-Pick
Lets you copy a single commit from one branch to another, allowing you to apply specific changes without merging entire branches.
```
git cherry-pick [commit1-hash] [commit-hash-2] ...
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
`git merge` preserves the original branching structure, while `git rebase` creates a cleaner, linear history by rewriting commit history. The choice between the two depends on the project's collaboration workflow and the desired commit history structure. <br><br>
Imagine you clone a repository on Monday and start dabbling on a side feature. By Friday you are ready to publish your feature -- but oh no! Your coworkers have written a bunch of code during the week that's made your feature out of date (and obsolete). They've also published these commits to the shared remote repository, so now your work is based on an old version of the project that's no longer relevant.

In this case, the command `git push` is ambiguous. If you run `git push`, should git change the remote repository back to what it was on Monday? Should it try to add your code in while not removing the new code? Or should it totally ignore your changes since they are totally out of date?

Because there is so much ambiguity in this situation (where history has diverged), git doesn't allow you to push your changes. It actually forces you to incorporate the latest state of the remote before being able to share your work.

How do you resolve this situation? It's easy, all you need to do is `base` your work off of the most recent version of the remote branch.
```
git pull --rebase
git push
```
Let's check out the same thing but with merge instead. 

Although git merge doesn't move your work (and instead just creates a merge commit), it's a way to tell git that you have incorporated all the changes from the remote. This is because the remote branch is now an ancestor of your own branch, meaning your commit reflects all commits in the remote branch.
```
git pull
git push
```
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
- ### Fetch vs Pull
`git pull` is essentially a combination of `git fetch` followed by `git merge`. <br>
`git fetch` when you want to see what changes have been made in the remote repository without integrating them into your local branch immediately. It's useful for reviewing changes before merging or rebasing. <br>
`git pull` when you want to fetch changes from the remote repository and automatically merge them into your current working branch. It's convenient for quickly updating your local branch with changes from the remote repository.
- ### Main Commits Rejection
If you work on a large collaborative team and you commit directly to main locally and try pushing you will be greeted with a message similar to this:
```
! [remote rejected] main -> main (TF402455: Pushes to this branch are not permitted; you must use a pull request to update this branch.)
```
The remote rejected the push of commits directly to main because of the policy on main requiring pull requests to instead be used.
So the solution is to create another branch called feature and push that to the remote. Also reset your main back to be in sync with the remote.
```
git checkout -b feature
git add .
git commit -m "Implemented feature"
git push origin feature
git checkout main
git fetch origin
git reset --hard origin/main
```
However, if you don't have write access to the repository you should do the following instead:
1- Create a fork of the repository on your GitHub account.
2- Run the above commands.
3- Create a pull request as a contribution to the main repository.

## Git Origins
`Origin` in Git is a convenient label for the default remote repository from which you cloned your local repository, allowing you to interact with it easily using Git commands. <br>
`origin/main`: This type of branch is called a remote branch; remote branches have special properties because they serve a unique purpose.<br>
Remote branches reflect the state of remote repositories (since you last talked to those remote repositories). They help you understand the difference between your local work and what work is public -- a critical step to take before sharing your work with others. <br>
Remote branches have the special property that when you check them out, you are put into detached HEAD mode. Git does this on purpose because you can't work on these branches directly; you have to work elsewhere and then share your work with the remote (after which your remote branches will be updated).

To be clear: Remote branches are on your local repository, not on the remote repository.<br>
Lets check out a remote branch, make a commit and see what happens.
```
git checkout origin/main
git commit
```
git put us into detached HEAD mode and then did not update `origin/main` when we added a new commit. This is because `origin/main` will only update when the remote updates.

<br><br>
### I'm still in the process of learning Git! Whenever I pick up something new, I jot it down right here. Stay tuned for updates!
