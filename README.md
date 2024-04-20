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
## Git Branches
- ### Git Branches 
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


<br><br>
### Stay tuned for updates! Coming soon.
