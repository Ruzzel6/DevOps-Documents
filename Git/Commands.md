```
# git remote -v   //is a Git command that shows the remote repositories connected to your local Git repository.
# git remote add <remote-name> <repository-url>
# git remote add gha-repo https://github.com/Ruzzel6/reponame.  // Then merge the initial commit that repo had

Note: origin stays pointed at the original source repo the whole time — you only ever push to gha-repo, never origin, unless you specifically want to contribute back upstream (which you usually don't for a forked/customized project like this).

git remote -v
git remote add gha-repo https://github.com/Ruzzel6/GitHub-Action-Opentelemetery-project-EKS.git
git add .
git commit -m "your message"
git fetch gha-repo
git merge gha-repo/main --allow-unrelated-histories
git pull gha-repo main
git status
git push gha-repo main
```
```
###Git Branch
git checkout -b ci-check //To create and checkout on that branch
git checkout main   //Switch to main
git branch -d checkout //Delete the checkout branch
```
