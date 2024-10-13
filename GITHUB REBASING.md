GITHUB REBASING
When you have forked a repo and commited and then discovered the original has also commited

git remote -v 
to check what branches and what is upstream

git remote add upstream ORIGINAL_REPO_URL
to add the upstream location

git fetch upstream
to get what happened upstream

git checkout main
to be sure on main branch

git rebase upstream/main

