# Git notes

## Create a new repository

Create a new directory, open it and perform a

`git init`

to create a new git repository.

## Clone a remote repository

In other words, create a working directory (or copy, or version) of a remote repository.
You will need to add more explanation here.

`git clone username@host:/path/to/repository`

E.g. `git clone https://github.com/guitarbeerchocolate/goldenratio.git`

When your repository is public (the default on GitHub), you don't need to put the username before the path.

## Clone a local repository

In other words, create a working directory (or copy, or version) of a local repository. The working copy is the one you play with.
You will need to add more explanation here.

`git clone /path/to/repository`

## How to check what you have changed in the working directory

`git status`

## Add files from the Working directory to the 'Index' or 'staging' area

You can do this either by filename E.g.

`git add myfile.php`

Or you can use wildcards E.g.

`git add *`.

You can check that the index has been updated using the command

`git diff --staged`

## Add files from the 'staging area' (Index) to the Head using 'commit'

Use the following command:

`git commit -m "Your message"`

## Switch to a branch

`git checkout master`

## Merge a branch

First checkout the branch you'd like to merge into, then:

`git merge email`

## Delete a branch

`git branch -d email`

## Use the 'push' command to send your commits to the remote repository

First check your config file. This should be in your working directory, within .git/config

You need to add the username and password to the url under '[remote "origin"]'.

Once you're all set up you can use the command:

`git push origin master`

## Push your branch to the remote repository

`git push origin email`

## Use 'pull' to update your local repository from remote version

To update your local repository to the newest commit use the command:

`git pull`

## Check the name of the remote repository (usually, it will be 'origin')

`git remote`

## Revert merges

This command will take you to the last merge:

`git revert HEAD`

This command will take you to the merge you made before last:

`git revert HEAD-2`

## Stashing

Let's assume that you got part way through some code, but you're not ready to commit. You just want to stash them and re-introduce them a little later.

This can also be useful if you temporarily need to change branch because another request has come in.
To stash your recent changes:

`git stash save "Some short comment about what I want to stash"`

See what's been stashed:

`git stash list`

This may provide example output such as:

`stash@{0}: "My message"`

In order to bring these example stashed changes back into our code we would use a command like this:

`git stash apply stash@{0}`

This will retain the stashed item within the list. If we want to take the stash at the top of the list, apply it to our code and remove it from the stash list we would use the command:

`git stash pop`

## Cherry picking

Cherry picking can be used to bring code in from a specific commit within a branch (rather than the whole branch). Let's assume we have a master branch and a branch called jimmy. In this example we'd like to bring a commit from the jimmy branch into the master branch, without merging the whole branch. We'll begin by checking out the jimmy branch:

`git checkout jimmy`

Now, if we get the log of jimmy we'll get a list of the commits made within the jimmy branch.

`git log`

From this list, we can then get the ID of the commit we'd like to use. We need to copy this ID.

We then need to switch back to master:

`git checkout master`

Now we can cherry pick the commit whose ID we have copied. This will also create a commit within master. You could also add several commit ID's within this command.

`git cherry-pick <IDs>`

If you want to cherry pick commits from another branch without committing them to your branch to check if they're OK first use:

`git cherry-pick <IDs> -n`

## Resolve conflict from pull request to Develop

Make sure you're on the branch which you created the pull request from:

`git branch`

`git pull origin Develop`

Edit out the conflicts

`git add <path of the file containing the conflicts>`

`git commit -m "Resolved conflict"`

`git push origin <branch which you created the pull request from>`

## What is origin?

It is an alias given to the URL pointing to the default remote repository.

## What is master?

The name of the default branch that git creates for you when first creating a repository. Your local repository has its own master branch, that almost always follows the master of a remote repository.

## What is a branch?

A branch is a variation of your code.
You create a branch from a repository when you need to work on an additional element. For example let's say you had to work on the email class.

## What is a fork?

A fork is a copy of a repository. Forking a repository allows you to freely experiment with changes without affecting the original project. Most commonly, forks are used to either propose changes to someone else's project or to use someone else's project as a starting point for your own idea.

## What's the difference between a branch and a fork?

When you fork a respository you also make a copy of all the branches in that repository.

## How the workflow works

There are 3 instances of a project which you will be exposed to.

- The **Working directory** is your copy or version to work on. From here you will perform 'add' commands in order to put your changes to the 'Index' or 'staging' area.
- The **Index** is the staging area. It is the index of your local working directory. From here you will perform 'commit' commands in order to put your changes to the 'Head' or 'the most recent commit' area.
- The **Head** contains the last commit you made. It is the head of your local working directory. 'Head' always refers to the most recent commit on the current branch. When you change branches, Head is updated to refer to the new branch's latest commit. **Note : ** making this commit does not push/send the commits to the remote repository for this you will need to use the 'push' command.
