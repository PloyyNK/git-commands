## Using Git

[Basics](#basics)    
[Adding and Changing Things](#adding-and-changing-things)    
[Undo Changes and Recover Files](#Undo-Changes-and-Recover-Files)  
[Viewing Commits](#Viewing-commits)    
[Commands for Remotes](remote-commands.md)   
[Favorites](#favorites)     
[Resources](#resources)

#### Note on Paths

In this file, directory paths are written with a forward slash as on MacOS, Linux, and the Windows-Bash shell: `/dir1/dir2/somefile`.    


## Basics

1. When using Git locally, what are these?  Define each one in a sentence
   * Staging area - (or can be called 'Index') Files and changes that marked to be commit next.
   * Working copy - A copy of an existing Git repository.
   * master - The default branch name in Git.
   * HEAD - A pointer to the local branch you're currently working on.


2. When you install git on a new machine (or in a new user account) you should perform these 2 git commands to tell git your name and email.  These values are used in commits that you make:
   ```
   git config --global user.name "your-name"
   git config --global user.email "your-email"
   ```

3. There are 2 ways to create a local Git repository.  What are they?
   - `git clone`: clone the existing Git repository
   - `git init`: create a new repository
   

4. When you create a git repository by entering `git init`, Git will create a "hidden" directory for the local repository.  Where is the directory for this local repository (relative to the directory where you typed "git init")?

   - It will create a subdirectory named `.git` that contains all of your necessary repository files.


## Adding and Changing Things

Suppose your working copy of a repository contains these files and directories:
```
README.md
out/
    a.exe
src/a.py
    b.py
    c.py
test/
    test_a.py
    ...
```

1. Add README.md and *everything* in the `src` directory to the git staging area.
   ```
   git add README.md
   git add src
   ```

2. Add `test/test_a.py` to the staging area (but not any other files).
   ```
   git add test/test_a.py
   ```

3. List the files in the staging area.
   ```
   git diff --staged
   ```
4. Remove `README.md` from the staging area. (Useful if you accidentally add something you don't want to commit.)
   ```
   git reset HEAD README.md
   ```

6. Commit everything in the staging area to the repository.
   ```
   git commit -m 'Initial commit'
   ```

7.Describe 2 steps to configure the repository so git will ignore all files in the `out/` directory:
   - step one: create a file named `.gitignore`. 
   - step two: put `out/` to ignore the directory and commit the file.

8.Command to move all the .py files from `src` to the top-level directory of this repository, so they are also moved in the Git repo.
   ```
   git mv src/* .
   ```

9.Commit this change with the message "moved src directory":
   ```
   git commit -m "moved src directory"
   ```
10.Command to add **all changed files** (but not untracked files) to the staging area using a single command.
   ```
   gid add -u
   ```

11.**Delete** the file `c.py` from your working copy **and** the repository:
   ```
   git rm c.py
   ```



## Undo Changes and Recover Files


1. Display the differences between your *working copy* of `a.py` and the `a.py` in the *local repository* (HEAD revision):
   ```
   git diff HEAD a.py
   ```
2. Display the differences between your *working copy* of `a.py` and the version in the *staging area*. (But, if a.py is not in the staging area this will compare working copy to HEAD revision):
   ```
   git diff 
   ```
3. **View changes to be committed:** Display the differences between files in the staging area and the versions in the repository. (You can also specify a file name to compare just one file.) 
   ```
   git diff --staged
   ```

4. **Undo "git add":** If `main.py` has been added to the staging area (`git add main.py`), remove it from the staging area:
   ```
   git restore --staged main.py
   ```

5. **Recover a file:** Command to replace your working copy of `a.py` with the most recent (HEAD) version in the repository.  This also works if you have deleted your working copy of this file.
   ```
   git checkout -- a.py
   ```

6. **Undo a commit:** Suppose you want to discard some commit(s) and move both HEAD and "master" to an earlier revision (an earlier commit)  Suppose the git commit graph looks like this (`aaaa`, etc, are the commit ids)
   ```
   aaaa ---> bbbb ---> cccc ---> dddd [HEAD -> master]
   ``` 
   The command to reset HEAD and master to the commit id `bbbb`:
   ```
   git reset --hard HEAD^2
   ```

7. **Checkout old code:** Using the above example, the command to replace your working copy with the files from commit with id `aaaa`:
   ```
   todo your answer here
   ```
    Note:
    - Git won't let you do this if you have uncommitted changes to any "tracked" files.
    - Untracked files are ignored, so after doing this command they will still be in your working copy.
 

## Viewing Commits

1. Show the history of commits, using one line per commit:
   ```
   git log --oneline
   ```
   Some versions of git have an *alias* "log1" for this (`git log1`).

2. Show the history (as above) including *all* branches in the repository and include a graph connecting the commits:
   ```
   git log --graph
   ```

3. List all the files in the current branch of the repository:
   ```
   git ls-files
   ```
   example output:
   ```
   .gitignore
   README.md
   a.py
   b.py
   test/test_a.py
   test/test_b.py
   ```


## Branch and Merge

> TODO write the commands to do each of these
1. Create a new branch named `dev-foo`:
   ```
   git checkout -b dev-foo
   ```
 
2. Display the name of your current branch:
   ```
   git branch –show-current
   ```

3. List the names of **all** branches, including remote branches:
   ```
   git branch -a
   ```

4. Switch your working copy to the branch named `dev-foo`:
   ```
   git checkout dev-foo
   ```

6. **Merge:** To merge the work from `dev-foo` into the master branch, perform these steps:
   1. step one
      ```
      git checkout master
      ```
   2. step two
      ```
      git merge dev-foo
      ```


6. Describe under what conditions a merge may fail.
   ```
   Failure of merge may have cause when two peoplework on the same line but 
   one deleted a file while the other modifying it. Git can't decide which 
   one is correct. This conflict will make the Git mark the file as being 
   conflicted and stop the merging process.
   ```


## Favorites

- Create new directory: `mkdir <file-name>`

---
## Resources

[Git Guides](https://github.com/git-guides) Guides to Git from start to advanced commands and workflows.

[Pro Git Online Book][ProGit] Chapters 2 & 3 contain the essentials. Downloadable PDF is also available.     
[Visual Git Reference](https://marklodato.github.io/visual-git-guide) one page with illustrations of git commands.

Try Git:

[Learn Git Interactive Tutorial][LearnGitInteractive] excellent visual tutorial.   
[Git Visualizer][VisualizeGit] execute Git commands in a web browser and see the results as a graph.    

[ProGit]: https://www.git-scm.com/book/en/v2 "Pro Git online book on Git-scm.com"
[ProGitPdf]: https://progit2.s3.amazonaws.com/en/2016-03-22-f3531/progit-en.1084.pdf "Pro Git v.2 PDF on AWS. Longer, book format."
[LearnGitInteractive]: https://learngitbranching.js.org "Interactive graphical git tutorial"
[VisualizeGit]: http://git-school.github.io/visualizing-git/ "Online tools draws a graph of commits in a repo as you type"
[markdown-cheatsheet]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[github-markdown]: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax
[vscode-markdown-preview-enhanced]: https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced
