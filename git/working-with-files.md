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
	hello-world.py

nothing added to commit but untracked files present (use "git add" to track)
$ git add hello-world.py
```

- Commit the changes to the repository

```
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   hello-world.py

$  git commit -m "Add hello world"
[master (root-commit) 9a1c4a6] Add hello world
 1 file changed, 4 insertions(+)
 create mode 100644 hello-world.py
$ git status
On branch master
nothing to commit, working tree clean
```

- Read and Use [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)

- Show the history of your changes to the repository

```
$ git log
git log
commit f680176183cb2d744b8e48538c0e6480649b5b35 (HEAD -> master)
Author: Walter Reiner <walter.reiner@wreiner.at>
Date:   Sun Jan 5 13:55:02 2020 +0100

    Add hello world
```

#### Change a file and commit changes to the repository

- Change the file in the Working Directory

```
$ sed -i 's/World/Course/' hello-world.py 
```

- Show the differences between the Working Directory and the repository

```
$ git diff
diff --git a/hello-world.py b/hello-world.py
index 6aeaccc..d235394 100644
--- a/hello-world.py
+++ b/hello-world.py
@@ -1,4 +1,4 @@
 #!/usr/bin/env python

 if __name__ == "__main__":
-    print("Hello World!");
+    print("Hello Course!");
```

- Check the status before commiting the changes

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   hello-world.py

no changes added to commit (use "git add" and/or "git commit -a")
```

- Add the changes to the Staging Area

```
$ git add hello-world.py
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hello-world.py

```

- Commit the changes to the repository

```
$ git commit -m "Change World to Course"
[master e0d06ef] Change World to Course
 1 file changed, 1 insertion(+), 1 deletion(-)
```

- You can skip the *git add* command and explicitly name all files which should be commited to the *commit* command:

```
$ git commit -m "Change World to Course" hello-world.py
```

- To stage all changes automatically, you can omit the *git add* command and use *-a*

```
$ git commit -m "Change greeting" -a
```

