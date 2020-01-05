# Git and Ansible Crash Course

Onboarding crash course by [Walter Reiner](mailto:walter.reiner@wreiner.at).

## Git

1. Git vs Github
1. Configure Git
1. Create a repository
1. Add the first file

### Git vs Github

#### Git
- Git is a version control system
    - **free and open source**
    - **distributed**
- [Tutorials](https://lala.com)

#### Github
- GitHub is a hosting service for Git repositories
- [Github](https://github.com)
- Most known alternative is [GitLab](https://gitlab.com)

### Configure Git

- Two essential settings that are required:

```
$ git config --global user.name "Your Name Comes Here"
$ git config --global user.email you@yourdomain.example.com
```

- Used in Git history

### Create a Git repository

- New project

```
$ mkdir new-project; cd new-project
$ git init
git init
Initialized empty Git repository in /home/wreiner/playground/new-project/.git/
```

- In an existing project

```
$ tar xvfz existing-project.tar.gz; cd existing-project
$ git init
Initialized empty Git repository in /home/wreiner/playground/existing-project/.git/
```

- From a hosting environment
    - Create the project on the hosted provider
        - Maybe add a README.md
    - Get the clone url of the repository
    - Clone the repository to your disk

    ```
    $ git clone git@gitlab.com:wreiner/ansible-crashcourse.git
    Cloning into 'ansible-crashcourse'...
    remote: Enumerating objects: 3, done.
    remote: Counting objects: 100% (3/3), done.
    remote: Compressing objects: 100% (2/2), done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Receiving objects: 100% (3/3), done.
    ```

### Work with files

#### Working Directory - Staging Area - Repository

- [Explanation with images](https://git-scm.com/about/staging-area)
- Files live in Working Directory
- Newly added or changed files live in the Staging Area
- Commited files live in the Repository

#### Adding a new file to the repository

- Start a git repository

```
$ mkdir new-project; cd new-project
$ git init
git init
Initialized empty Git repository in /home/wreiner/playground/new-project/.git/
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```
- Create the file with its contents (Working Directory)

```
$ cat <<NPF >> hello-world.py
#!/usr/bin/env python

if __name__ == "__main__":
    print("Hello World!");
NPF
$ cat hello-world.py
$ python hello-world.py
```

- Add the file to the Staging Area

```
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	test.py

nothing added to commit but untracked files present (use "git add" to track)
$ git add test.py
```

- Commit the changes to the repository

```
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   test.py

```
