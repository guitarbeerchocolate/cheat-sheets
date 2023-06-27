#Git notes

##Create a new repository
Create a new directory, open it and perform a
`git init`
to create a new git repository.

##Clone a remote repository
In other words, create a working directory (or copy, or version) of a remote repository.
You will need to add more explanation here.
`git clone username@host:/path/to/repository`
E.g. `git clone https://github.com/guitarbeerchocolate/goldenratio.git`
When your repository is public (the default on GitHub), you don't need to put the username before the path.

##Clone a local repository
In other words, create a working directory (or copy, or version) of a local repository. The working copy is the one you play with.
You will need to add more explanation here.
`git clone /path/to/repository`

##How to check what you have changed in the working directory
`git status`

##Add files from the Working directory to the 'Index' or 'staging' area
You can do this either by filename E.g. `git add myfile.php`
Or you can use wildcards E.g. `git add *`.
You can check that the index has been updated using the command
`git diff --staged`

##Add files from the 'staging area' (Index) to the Head using 'commit'
Use the following command
`git commit -m "Your message"`

##Switch to a branch
`git checkout master`

##Merge a branch
First checkout the branch you'd like to merge into, then:
`git merge email`

##Delete a branch
`git branch -d email`

##Use the 'push' command to send your commits to the remote repository
First check your config file. This should be in your working directory, within
.git/config
You need to add the username and password to the url under '[remote "origin"]'.
Once you're all set up you can use the command
`git push origin master`

##Push your branch to the remote repository
`git push origin email`

##Use 'pull' to update your local repository from remote version
To update your local repository to the newest commit use the command
`git pull`

##What is origin?
It is an alias given to the URL pointing to the default remote repository.

##What is master?
The name of the default branch that git creates for you when first creating a repository. Your local repository has its own master branch, that almost always follows the master of a remote repository.

##What is a branch?
A branch is a variation of your code.
You create a branch from a repository when you need to work on an additional element. For example let's say you had to work on the email class.

##What is a fork?
A fork is a copy of a repository. Forking a repository allows you to freely experiment with changes without affecting the original project. Most commonly, forks are used to either propose changes to someone else's project or to use someone else's project as a starting point for your own idea.

##What's the difference between a branch and a fork?
When you fork a respository you also make a copy of all the branches in that repository.

##How the workflow works
There are 3 instances of a project which you will be exposed to.

- The **Working directory** is your copy or version to work on. From here you will perform 'add' commands in order to put your changes to the 'Index' or 'staging' area.
- The **Index** is the staging area. It is the index of your local working directory. From here you will perform 'commit' commands in order to put your changes to the 'Head' or 'the most recent commit' area.
- The **Head** contains the last commit you made. It is the head of your local working directory. 'Head' always refers to the most recent commit on the current branch. When you change branches, Head is updated to refer to the new branch's latest commit. **Note : ** making this commit does not push/send the commits to the remote repository for this you will need to use the 'push' command.
