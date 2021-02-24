With GitHub, there are commands that I use all the time. Such as:

```
$ git clone
$ git init
$ git status
$ git add .
$ git commit -m '${insert message here}'
$ git push
```

But sometimes I do run into the same errors all the time! But I never remember how to fix them because I don't fully understand it! So what are those errors?


## Branching

```
$ git branch // List branches
$ git branch -a // List all remote branches
$ git branch <new_branch> // Create new branch
$ git branch -d <branch> // Delete branch
$ git branch -D <branch> // Force delete branch
$ git branch -m <rename_branch> // Rename branch

$ git checkout <branch> // Change current branch
$ git checkout -b <new_branch> // Create and change current branch
```

A local branch is a branch that only you (the local user) can see. It exists only on your local machine. A remote branch is a branch on a remote location (in most cases origin). You can push the newly created local branch myNewBranch to origin. Now other users can track it.

When it comes to deleting branches, by replacing -d with -D, you are telling git to delete the branch and that you don't care to merge changes from that branch. The -d flag is an alias for --delete, which only deletes the branch if it has already been fully merged in its upstream branch. You could also use -D, which is an alias for --delete --force, which deletes the branch "irrespective of its merged status."

