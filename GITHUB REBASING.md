GITHUB REBASING
When you have forked a repo and commited and then discovered the original has also commited
Or when you want to pull some edits from the original source and keep your changes- pulling your changes on top of some other source

git remote -v 
to check what branches and what is upstream

git remote add upstream ORIGINAL_REPO_URL
to add the upstream location

git fetch upstream
to get what happened upstream

git checkout main
to be sure on main branch

git rebase upstream/main

After this you will have some merge conflicts to solve but
 there is also git rebase --continue, after solving the conflicts

 after this is really important to commit and push so that the changes are updated in repo

