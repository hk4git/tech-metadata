###### Clear - clean up unnecessary files and optimize the local repository
`git gc --prune=now` - Get error/warnings like: error: cannot lock ref etc...

###### Directly clone from specific branch from remote repo: this will create direct branch locally, make sure to at remote repo only
`git clone -b <branch-name> <repository-url>`

###### Check if your local/current branch points to which remote origin?
`git branch -avv`	=> shows For all branches
`git branch -lvv`	=> For local branches only.
 
###### How to Preserve Local Changes Before Checkout-
 + Preserve local changes using -> `git stash`
 + temporary branch, or
 + commit.

###### REBASE: to keep clean with change history
`git rebase origin/main`

##### How to resolve issues:
 + ###### "Your branch is ahead of 'origin/main' by 1 commit":
	Before deciding whether to push or undo the commit, you may want to review the differences between your local branch and the remote branch `git diff origin/main`
	+ `git reset --soft HEAD~1`	=> Soft reset (keeps changes staged, resets the branch to the previous commit but keeps your changes staged)
	+ `git reset HEAD~1`	=> Mixed reset (keeps changes but unstaged, resets the branch to the previous commit and unstages the changes)
	+ `git reset --hard HEAD~1`	=> Hard reset (discards changes, resets the branch to the previous commit and discards all changes)

+ ###### Error "fatal: '' is not a commit and a branch '' cannot be created from it"
	`git fetch --all`

+ ###### HOW TO MERGE DEV to MASTER
  	- `git merge master` - (on branch development), (resolve any merge conflicts if there are any 
	- `git checkout master`
	- `git merge development` (there won't be any conflicts now) | git merge --no-ff development {merge creates a commit by default}


#### Cherry-pick
 `git cherry-pick` This command allows you to apply specific commits from one branch to another. Only your changes from the dev branch to the main branch, you can use the.
1) Identify your commits: First, find the commit hashes of your changes in the dev branch.
2) Switch to the main branch: `git checkout main`
3) Pull the latest changes from the remote main branch to ensure your local main branch is up-to-date: `git pull origin main`
4) Cherry-pick your commits: Apply your specific commits to the main branch using their commit hashes: `git cherry-pick <commit_hash1> <commit_hash2> ...`
5) Resolve any conflicts if they arise during the cherry-pick process. After resolving conflicts, add the resolved files:
`git add <resolved_file>`
`git cherry-pick --continue`
6) Push the changes to the remote main branch: `git push origin main`

Example
Start the cherry-pick:`git cherry-pick d6f0fb`
Resolve conflicts: `git add <resolved-file>`
Continue the cherry-pick: `git cherry-pick --continue`
If you want to abort the cherry-pick: `git cherry-pick --abort`

### Leverage Git Hooks:
Git hooks are scripts that can be executed automatically during various Git events, such as pre-commit, pre-push, or post-checkout.


## TO - CHECK
- IS ISSUE IN GIT?: If we rebase current branch (current changes) with origin/main, for whihch PR was already raised and merged, then current changes also gets commited automatically without PR
- Should we keep different local clone for diffent remote origin ???
