# Git Crash Course

Onboarding crash course for Git.

## Git

1. Git vs Github
1. Configure Git
1. Create a repository
1. Working with files
1. Working with remote repositories
1. Working with branches

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
