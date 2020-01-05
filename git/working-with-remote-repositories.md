### Working with remote repositories

#### Clone a remote repository

```
$ git clone git@gitlab.com:wreiner/example-repo.git
Cloning into 'example-repo'...
warning: You appear to have cloned an empty repository.
```

#### Remotes

- A repository can have multiple remotes
- Each remote has a name
- Standard remote is named *origin*

```
$ cd example-repo
$ git remote -v
origin	git@gitlab.com:wreiner/example-repo.git (fetch)
origin	git@gitlab.com:wreiner/example-repo.git (push)
```

#### Commit changes

- Make some changes, i.e. add a file

```
$ touch README.md
$ git add README.md
$ git commit -m "add README"
```

- Changes are still only in the local repository

#### Push changes to the remote repository

- Every git repository has a standard branch called *master*
- To circumvent merge conflicts, **ALWAYS** *pull* before *push*
- To get the changes to the remote repository, *push* the changes of the branch *master* to the remote *origin*

```
$ git pull
$ git push -u origin master
```

#### Push an existing folder

```
$ cd existing_folder
$ git init
$ git remote add origin git@gitlab.com:wreiner/example-repo.git
$ git add .
$ git commit -m "Initial commit"
$ git push -u origin master
```

#### Push an existing Git repository

```
$ cd existing_repo
$ git remote rename origin old-origin
$ git remote add origin git@gitlab.com:wreiner/example-repo.git
$ git push -u origin --all
$ git push -u origin --tags
```

