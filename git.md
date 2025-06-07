git gc --prune=now 

Directly clone from specific branch from repo:
git clone -b <branch-name> <repository-url>


Should we keep different local clone for diffent remote origin ???

Check if your local/current branch points to which remote origin?
git branch -avv	=> shows For all branches
git branch -lvv => For local branches only.
 
-Preserving Local Changes Before Checkout-
Preserve local changes using -> stash, temporary branch, or commit.

REBASE: to keep clean with change history
=>git rebase origin/main


"Your branch is ahead of 'origin/main' by 1 commit" check below --
Before deciding whether to push or undo the commit, you may want to review the differences between your local branch and the remote branch
git diff origin/main
git reset --soft HEAD~1	=> Soft reset (keeps changes staged, resets the branch to the previous commit but keeps your changes staged)
git reset HEAD~1	=> Mixed reset (keeps changes but unstaged, resets the branch to the previous commit and unstages the changes)
git reset --hard HEAD~1	=> Hard reset (discards changes, resets the branch to the previous commit and discards all changes)

How to resolve git error "fatal: '' is not a commit and a branch ' cannot be created from it"
Ans: git fetch --all

MERGE DEV to MASTER
- (on branch development)$ git merge master
	(resolve any merge conflicts if there are any)
- git checkout master
- git merge development (there won't be any conflicts now) | git merge --no-ff development {merge creates a commit by default}


cherry-pick:
only your changes from the dev branch to the main branch, you can use the git cherry-pick command. This command allows you to apply specific commits from one branch to another.

1) Identify your commits: First, find the commit hashes of your changes in the dev branch.
2) Switch to the main branch: git checkout main
3) Pull the latest changes from the remote main branch to ensure your local main branch is up-to-date: git pull origin main
4) Cherry-pick your commits: Apply your specific commits to the main branch using their commit hashes: git cherry-pick <commit_hash1> <commit_hash2> ...
5) Resolve any conflicts if they arise during the cherry-pick process. After resolving conflicts, add the resolved files:
git add <resolved_file>
git cherry-pick --continue
6) Push the changes to the remote main branch:git push origin main

--
Start the cherry-pick:`git cherry-pick d6f0fb`
Resolve conflicts: `git add <resolved-file>`
Continue the cherry-pick: `git cherry-pick --continue`
If you want to abort the cherry-pick:`git cherry-pick --abort`


Leverage Git Hooks:
Git hooks are scripts that can be executed automatically during various Git events, such as pre-commit, pre-push, or post-checkout.

ISSUE?:
If we rebase current branch (current changes) with origin/main, for whihch PR was already raised and merged, then current changes also gets commited automatically without PR.
