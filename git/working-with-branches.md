### Working with branches

- [Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

#### What is a branch

list branches
push branches to remote

#### Create a branch

- Create a new branch - choose a meaningful name
    - feat-xxx = feature branch
    - hotfix-xxx = hotfix branch

```
$ git checkout -b feat-footer
Switched to a new branch 'feat-footer'
```

- Make some changes and commit them

```
$ gic -m "Add footer to index" -a
[feat-footer 0a24bd7] Add footer to index
 1 file changed, 3 insertions(+)
```

#### Pushing branch to remote

- Up until now the branch exists only in the local repository
- For various reasons it can be pushed to the remote
- Syntax is the same as with master branch

```
$ git push origin feat-footer
```

#### Switching between branches

- Switch back to master branch

```
$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
```

- Switch to the feature branch

```
$ git checkout feat-footer
Switched to branch 'feat-footer'
```

#### Merge feature branch into master

- First switch to branch you want to merge to

```
$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
```

- Merge the new feature branch

```
$ git merge feat-footer
Updating cb154e7..0a24bd7
Fast-forward
 index.html | 3 +++
 1 file changed, 3 insertions(+)
```

- Push the new master to the remote

```
$ git push
Total 0 (delta 0), reused 0 (delta 0)
To gitlab.com:wreiner/example-repo.git
   cb154e7..0a24bd7  master -> master
```

- Remove the local branch

```
$ git branch -d feat-footer
Deleted branch feat-footer (was 0a24bd7).
```

#### Merge commits

- Create a new feature branch

```
$ git checkout -b feat-newp
Switched to a new branch 'feat-newp'
```

- Make changes in the feature branch and commit them

```
$ gic -m "Added new text to index" -a
[feat-newp 9e0e736] Added new text to index
 1 file changed, 3 insertions(+)
```

- Checkout master and create a hotfix branch

```
$ git checkout master
$ git checkout -b hotfix-123
```

- Make changes in the hotfix branch and commit them

```
$ sed -i "s/someone/someteam/" index.html
$ git commit -m "Changed email address to team" -a
```

- Merge hotfix into master

```
$ git checkout master
$ git merge hotfix-123
Updating 0a24bd7..6fa6d7e
Fast-forward
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

- Now merge feature branch
    - This creates a merge commit because a simple fast forward is not possible

```
$ git merge feat-newp
```

#### Merge conflicts

- Git is really good at sovling merge conflicts
- Some conflicts cannot be resolved automatically

#### Create a merge conflict

- Create a new file in master

```
$ echo "echo Hello" > my_code.sh
$ git add my_code.sh
$ git commit -am 'Add new file'
```

- Create a new feature branch

```
$ git checkout -b feat-worldhello
$ echo "echo \"Hello World\"" > my_code.sh
$ git commit -m 'Add the world' -a
```

- Someone makes a change to the master branch
    - Either commiting in master branch directly or merging another branch into master

```
$ git checkout master
$ echo 'echo "Hello World!"' > my_code.sh
$ git commit -am 'Add the WORLD!'
```

- Merging in the feature branch will result in a merge conflict

```
$ git merge feat-worldhello
Auto-merging my_code.sh
CONFLICT (content): Merge conflict in my_code.sh
Automatic merge failed; fix conflicts and then commit the result.
```

#### Resolve a merge conflict

- Merge conflicts are visible in the following way

```
<<<<<<< HEAD
echo "Hello World!"
=======
echo "Hello World"
>>>>>>> feat-worldhello
```

- Change the file to the desired content
    - Remove <<< === >>> lines

```
# here the content of HEAD wins
echo "Hello World!"
```

- Commit the repaired file

```
$ git status
On branch master
Your branch is ahead of 'origin/master' by 5 commits.
  (use "git push" to publish your local commits)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   my_code.sh
$ git add my_code.sh
$ git status
On branch master
Your branch is ahead of 'origin/master' by 5 commits.
  (use "git push" to publish your local commits)

All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

$ git commit -m "Fix merge conflict" -a
[master 810736e] Fix merge conflict
$ git status
On branch master
Your branch is ahead of 'origin/master' by 7 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

