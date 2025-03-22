# DIT114 Git Tutorial

## Links

-   [Git Documentation](https://git-scm.com/docs)
-   [Git Cheatsheet](https://training.github.com)

## What is Git?

["git" can mean anything, depending on your mood.](https://github.com/git/git/blob/e83c5163316f89bfbde7d9ab23ca2e25604af290/README)

![](res/xkcd.png)
[xkcd.com/1597/](https://xkcd.com/1597/)

# Installing Git

Please refer to [git-scm.com](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for installation instructions.

## Installing Git via a Package Manager

### Windows

You can install Git via [Chocolatey](https://community.chocolatey.org/packages/git) on Windows.

### MacOS

There is a high chance that you already have Git installed. Try running this command to check:

```shell
git --version
```

If Git is not installed, you can install it via [Homebrew](https://brew.sh) using the command below.

```shell
brew install git
```

### Linux

Check what package manager your distro is using.

# Recommendations

Since Windows is not a UNIX-related system, we recommend Windows users to use **bash shell** that comes included with the Git installation.

MacOS and Linux users can use their terminal of choice, since both systems are UNIX or UNIX-like.

# Configuring Git (and GitLab)

To configure your username and email for all local repositories use these commands:

```shell
git config --global user.name "kamil" # set your git name to "kamil"
git config --global user.email "kamil@example.com" # set your git email to "kamil@example.com"
git config --global color.ui auto # extra config command to make stuff more readable
git config --global core.editor "nano" # set the default editor for git to nano (or whatever text editor you like)
```

**It is very important to set up your name and email correctly!** These settings are used by services like GitHub and GitLab to track your contributions correctly.

**Please either use your ChalmersID or if you want to use another email, go to your GitLab settings panel, and set up your email as the commit email.**

Then you can create an empty repository on GitLab and check if GitLab is tracking your commits correctly (i.e. if clicking on your name in the commit view moves you to your profile).

To check your global git config use this command:

```shell
git config --global --list
```

On GitLab, go to _profile_ and check what is your _Commit Email_ — it has to match the email address you use with Git.
![](res/git-workshop-18.png)

# Using Git

## Initializing Local Git Repository

-   First we will create a local Git repository on our computer.
-   To do this, open your terminal of choice (for Mac users I recommend [iTerm2](https://iterm2.com) or [Kitty](https://sw.kovidgoyal.net/kitty/) (both can be installed with [Homebrew](https://brew.sh)).
-   Use `mkdir` to create a new directory (folder), `cd` to change directory to your newly created one, and `git init` to initialize git repository.

![](res/git-workshop-1.png)

-   Use `touch` command to create a new file (`touch readme.md`).
-   You can use `ls` to list files in the current working directory.
    ![](res/git-workshop-2.png)
-   I will edit the newly created `readme.md` file using my preferred text editor. I will add _hello word!_ and save the changes.
    ![](res/git-workshop-3.png)
-   I edited the file in vim using `nvim readme.md` command (you can use `nano`, VS Code, etc.).
-   Then I use `git status` to see the current status of the repository. As you can see on the attached image below, it tells me that I am on branch 'main', that there are no commits yet, and that there is one untracked file on the branch.
-   Untracked files are files that Git will not include in our repository.
-   `Git status` command suggests using `git add` to start tracking files. Let's do that!
    ![](res/git-workshop-4.png)
-   I use `git add readme.md` to add `readme.md` file to be tracked.
-   Now when I type in`git status`, it will tell me that `readme.md` is tracked.
-   From now on, Git will include that file in the repository.
    ![](res/git-workshop-5.png)

## Committing

-   Now let's commit our file (i.e. save a version of that file).
-   Sounds familiar? I know it does.
    -   _"submission.pdf"_,
    -   _"copy of submission final.pdf"_,
    -   _"copy of copy of submission final this one.pdf"_,
    -   _"copy of copy of copy of submission final this one is the correct one"_
-   Committing in Git is exactly that, but Git manages the versioning for you.
    ![](res/xkcd-2.png)
    [xkcd.com/1296](https://xkcd.com/1296/)

### Committing Files

-   Use `git commit -m "commit message goes here"` to commit the tracked files.
    ![](res/git-workshop-6.png)
-   Use `git log` to see the log of commits.
-   Each commit has a hash, that acts as a unique identifier.  
    ![](res/git-workshop-7.png)
-   Now let's change the file again. I will change line 3 to _"I love DIT114"_ and save the file.
    ![](res/git-workshop-9.png)
-   I use `git status` to check the status.

![](res/git-workshop-10.png)

-   And `git add .` to add all files to be tracked (`.` — current working directory).
-   Then I `git status` again to see what files are tracked.
-   Then I use `git commit` to commit my changes.
    ![](res/git-workshop-12.png)
-   Use `git log` to see the commit log.
    ![](res/git-workshop-13.png)
-   Then use `git diff <hash> <hash>` to compare two commits **(the order of hashes matters!)**
    ![](res/git-workshop-16.png)
-   `git diff ee7c8ad fb163e3` (bad)
    ![](res/git-workshop-15.png)
-   `git diff fb163e3 ee7c8ad` (good)
    ![](res/git-workshop-17.png)

## Connecting to a Remote

### What is a Remote?

-   Git is like email, it is a technology, protocol.
-   A _Local_ is your local repository, so files on your computer.
-   A _Remote_ is like Google Drive, iCloud, OneDrive, etc.
-   In our case the Remote is GitLab.

### Pushing to a Remote

-   First you need to tell Git that it should upload your files to your remote.
-   Tip: If you create an empty repository on GitLab or GitHub, there is a tutorial how to connect a remote.
    ![](res/git-workshop-19.png)
-   Connecting to a remote is easy. Use `git remote add origin <remote address>`.
-   You can get the address of the remote, from the repo. Go to the repo, and click "code" and copy the address.
-   Alternatively, you can use `git clone <remote address>` to 'download' the remote to your computer (more common than initializing repos locally first).
    ![](res/git-workshop-20.png)
-   Now Git knows what my remote is.
-   Use `git push --set-upstream origin main` to push your committed changes.
-   After that, you don't have to type in `--set-upstream...`, just use `git push`.
    ![](res/git-workshop-21.png)

### Common Problems

#### Pulling Remote and Sync Conflicts

-   Let's edit our file on the remote. I will change the 3rd line to something different.
    ![](res/git-workshop-22.png)
-   Now committing it...

![](res/git-workshop-23.png)

-   And done!
    ![](res/git-workshop-24.png)
-   I open the file on my computer and... no changes! What happened?
    ![](res/git-workshop-26.png)
-   Well, we need to `pull` the changes from the remote to the local repo.
-   Use `git pull` to do that.
    ![](res/git-workshop-28.png)
-   And now our local is in sync with the remote.

![](res/git-workshop-29.png)

-   And if I open the file, the changes are there.
    ![](res/git-workshop-30.png)

#### Merge Conflicts

-   Let's edit the file on the remote again.
-   I will change the 3rd line one more time.
    ![](res/git-workshop-31.png)
-   Committing...
    ![](res/git-workshop-33.png)
-   And now I will change the same file and the same line on my local, without pulling the remote first.

![](res/res/git-workshop-34.png)

-   I add and commit my changes, and I try to push it.
-   Whoops! What is happening? Scary!
-   We have a conflict. The file was edited on the same line, both on the remote and local, and now Git does not know which change is the correct one.
    ![](res/git-workshop-35.png)
-   Ok. Let's try pulling the remote...
-   Git explains what is happening and suggests actions that we can take.
-   I will go with the first one `git config pull.rebase false`, which will result in a merge request between the two versions of the file.
-   This way, I can see both changes and decide what the merged file should include.
-   How should I know which option to pick? It all depends on the developer preference and the situation.
    ![](res/git-workshop-36.png)
-   I tell Git what to do and pull again. Now it created a merge conflict that I have to resolve.
    ![](res/git-workshop-37.png)
-   I will use Visual Studio Code to resolve the conflict. You can use `code .` command to open the current working directory in VSCode.
    ![](res/git-workshop-38.png)

-   Resolving conflicts in the Merge Conflict Manager.

![](res/git-workshop-39.png)

-   Committing the changes...

![](res/git-workshop-40.png)

-   Now I can push to remote.

![](res/git-workshop-41.png)

-   And it is pushed!

![](res/git-workshop-42.png)

## Branching

Will help you avoid the aforementioned issues.

-   Use `git branch <branch-name>` to create a branch. The branch will be created from the current active branch you're on.
-   Use `git checkout <branch-name>` to switch to a branch.
    ![](res/git-workshop-44.png)
-   I edit the file on the newly created branch.
    ![](res/git-workshop-45.png)
-   Then, I add and commit my changes, and push it to the remote.

![](res/git-workshop-46.png)

-   Git tells me that I can create a new merge (a.k.a pull request).
-   A merge requests is when you join one branch into another (e.g. feature —> main).
    -   It is a common practice to 'delete' a feature branch after it is merged.
    -   _We usually merge a feature branch to a develop branch, and develop to main._
-   You can merge branches locally, and then push the changes to the remote, but we recommend using GitLab for it.
    ![](res/git-workshop-49.png)
-   And it is merged.

![](res/git-workshop-50.png)

-   Don't forget to pull the changes from the remote to your local repository and switch the branch.
    ![](res/git-workshop-51.png)
-   And that is all!
-   At the top of this page I leave additional resources about Git.
-   The best way to learn, is to practice. Create a test repository on your GitLab and try out the above steps yourself.
