# Git Commands
`git` is a command line application for source control.  
GUIs exist, but still just run commands for you, and display the output nicely.  
Most developers will at some point need to run some git commands.

I do suggest getting a git GUI (not GitHub's, it kinda sucks).  
The primary benefit of a good GUI is to make it so you don't need to memorize these and 100s of other commands.  

Some good Git GUIs: 
- TortoiseGit: https://tortoisegit.org/ (unfortunately, Windows Only)
- GitExtensions: https://gitextensions.github.io/ (Windows/Linux/Mac)
- SourceTree: https://tortoisegit.org/ (Windows/Mac Only)

## Basic GIT Commands
### `git`ing started
[`git init`](#git-init)  
[`git clone`](#git-clone)  
### Basic operation
[`git status`](#git-status)  
[`git config`](#git-config)  
[`git add`](#git-add)  
[`git commit`](#git-commit)
[`git push`](#git-push)
[`git pull`](#git-pull)

### Slightly more advanced operation
[`git remote`](#git-remote)
[`git branch`](#git-branch)
[`git checkout`](#git-checkout)

# `git init`
Initializes a new repository in the current working directory (creates a `./.git` folder).  
Note, this starts with:
- no files tracked
- no remotes  
You will have to do all necessary steps to add remotes if you want to push your changes to a remote repository (eg, github)  
(see [`git remote`](#git-remotes))
```
λ pwd
C:\Dev\examples
λ git init
Initialized empty Git repository in C:/Dev/examples/.git/
```

# `git clone`
Downloads a copy of a repository, including all of its history, from a given url.  
Automatically sets up the location the repo was downloaded from as a remote.  
Creates a folder with the repository name by default. Can use various flags.
```
λ ls
examples/
λ git clone https://github.com/ninjapretzel/XtoJSON.git
Cloning into 'XtoJSON'...
remote: Enumerating objects: 188, done.
remote: Counting objects: 100% (188/188), done.
remote: Compressing objects: 100% (125/125), done.
Rremote: Total 521 (delta 124), reused 122 (delta 59), pack-reused 333
Receiving objects:  94% (490/521), 156.01 KiB | 293.00 KiB/s
Receiving objects: 100% (521/521), 300.43 KiB | 314.00 KiB/s, done.
Resolving deltas: 100% (334/334), done.
λ ls
examples/  XtoJSON/
```

# `git status`
Gives you a readout of the state of the repository (you must already be in a repository).  
Good to run this to confirm the state of the repository before running other commands.  

Example output:
```
λ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   ExServer/Core/Generator/Gen.cs
        modified:   ExServer/Program.cs
        modified:   db/ItemGeneration/Materials.wtf
        modified:   db/Items/Enhancement.wtf

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        codex.wtf
        db/Codex.wtf
        db/statPlan.wtf

no changes added to commit (use "git add" and/or "git commit -a")
```
You will see only the status of your own repository (which may be nothing changed:)
```
λ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

# `git config` 
Git requires some minimal configuration, to put some identity information with commits you make.  
To set these across your entire system, use:
```
λ git config --global user.name "Name"
λ git config --global user.email "yourmail@mailer.site"
```
If you want to change them in a per-repository basis, use 
```
λ git config user.name "Name"
λ git config user.email "yourmail@mailer.site"
```


# `git add`
This command lets you 'stage' files for commit.  
Staged files are what get committed with `git commit`, and you can leave some changes unstaged to leave them out of commits.
```
λ git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        basics/git.md
        basics/github.md

nothing added to commit but untracked files present (use "git add" to track)

λ git add basics\git.md

λ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   basics/git.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        basics/github.md
```

# `git commit`
This command lets you 'commit' staged changes. This creates a checkpoint that you can restore.  
You must provide a message, which can be done with the following:  
`$> git commit -m "Descriptive message"`
```
λ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   basics/git.md

λ git commit -m "Adds git commands file"
[master 3eb305f] Adds git commands file
 1 file changed, 139 insertions(+)
 create mode 100644 basics/git.md
```

# `git push`
Pushes up any commits to the remote repository.  
May fail if there are any changes on the remote repository that conflict with your changes...

How it looks when there are local changes the remote does not have yet:
```
λ git push
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 12 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 2.12 KiB | 2.12 MiB/s, done.
Total 4 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/ninjapretzel/guides.git
   a121bd4..3eb305f  master -> master
```

How it looks when there are no changes the remote has:
```
λ git push
Everything up-to-date
```

Can push specific branches up (see also [`git branch`](#git-branch) and[`git checkout`](#git-checkout))  
`git push REMOTE BRANCH`
```
λ git push origin master
Everything up-to-date
```

# `git pull`
Pulls down any changes from the remote repository, and applies them to the working directory.  
May fail if there are any changes on the remote repository that conflict with your changes...

Automatically tries to pull the changes from the same working branch on the default remote.
```
λ git pull
Already up to date.
```
For most purposes if you're on `master` already, the above is the same as:
```
λ git pull origin master
Already up to date.
```

# `git fetch`
Pulls changes down, but doesn't necessarily apply them to the working directory.  
Typically used to grab changes from different remotes.
```
λ git fetch --all
Fetching origin
```

# `git remote`
Used to manage remotes.
Typically you just need one, `origin`.  
Use this command if you prefer doing things the hard way, or if you need to work with multiple remotes for some reason (again, doing things the hard way.)  
To do the exact same thing that `git clone blah` will do, but in more steps, do  the following:
```
λ mkdir XtoJSON
λ cd XtoJSON
λ git init
Initialized empty Git repository in C:/Dev/examples/.git/
λ git remote add origin https://github.com/ninjapretzel/XtoJSON.git
λ git pull origin master
remote: Enumerating objects: 179, done.
remote: Counting objects: 100% (179/179), done.
remote: Compressing objects: 100% (114/114), done.
remote: Total 512 (delta 117), reused 122 (delta 61), pack-reused 333
Receiving objects: 100% (512/512), 294.25 KiB | 295.00 KiB/s, done.
Resolving deltas: 100% (327/327), done.
From https://github.com/ninjapretzel/XtoJSON
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master

```



# `git branch`
# `git checkout`
Commands used to create and manage branches.

Creating and using a branch: (new branch uses current working 'head')
```
λ git branch NewBranch

λ git checkout NewBranch
Switched to branch 'NewBranch'

λ git status
On branch NewBranch
nothing to commit, working tree clean
```

Both can be done at the same time:
```
λ git checkout -b AnotherNewBranch
Switched to a new branch 'AnotherNewBranch'
```

You can also delete a branch, this will remove it from the local repository.
```
λ git branch -d NewBranch
Deleted branch NewBranch (was 153bec2).
```

Switching to an existing branch will likely change/add/remove files in your working directory.
```
λ git checkout master
Switched to branch 'master'
```

