# Table of Contents
[**Introduction**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_edit#introduction)  
[**General Recommendations**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance#general-recommendations)    
[**Overview**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#overview)   
[**Local Initialization**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#local-initialization)   
[**Forks**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#forks)   
* Setting up Forks    
* Updating your Fork    
* Collaborators    

[**Clone, Commit, Branch**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#clone-commit-branch)   
* Creating a Sandbox (clone)    
* Commit    
* Branch    

[**Pushing and Pulling**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#pushing-and-pulling)   
* Remotes    
* Push    
* Pull    
* Pull Requests (PR)    

[**Submodules**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#submodules)   
* Overview    
* Modify Icepack code inside CICE    
* Modify and Commit Icepack Changes    
* Update the Icepack Version in CICE    
* Completely Remove and Replace the Icepack Submodule in CICE    

[**Information**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#information)   
* Status    
* Diff    
* Log    

[**Appendix A:** Table of useful git commands  (git [command])](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#appendix-a-table-of-useful-git-commands--git-command)   
[**Appendix B:** Best Practices](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#appendix-b-best-practices)   
[**Appendix C:** Terms](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#appendix-c-terms)   

***

# Introduction
This document provides a simplified overview of git and how to use it within CICE-Consortium development.  In most cases, it does not fully represent the details and complexity associated with git.  It should provide a starting point for working in the CICE-Consortium, and it will hopefully encourage users to look for more detailed documentation on the web.  This document is not a substitute for a proper and detailed git user guide.  

# General Recommendations
* _Create your own forks for each repository._

* Keep your fork master consistent with the Consortium master:
_pull from the Consortium master and push to your fork_  

* Work on branches in your sandbox, not on master.
Always branch from master unless you specifically want changes from another branch in the new branch.
Use different sandboxes for different branches.
_Never push changes to your fork master, only to branches._

* _Immediately before a Pull Request, [update your fork](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance#updating-your-fork) using the Consortium master as your upstream source._

* _Before a Pull Request run the appropriate tests (see [Resource Guide](https://github.com/CICE-Consortium/About-Us/wiki/Resource-Index#model-testing) for details) and post the results._

* _Break Pull Requests into multiple pieces (one "fix" at a time)._ Fill in the Pull Request template with details specific to each particular "fix". This is especially important if some changes are bit-for-bit and others are not. 

* Be very careful with every pull and push command to make sure it's from/to the right repo/fork/branch and contains what is intended.  
_Use ‘git status’ and ‘git remote -v’ frequently._

See also our [Software Development Practices](https://github.com/CICE-Consortium/About-Us/blob/master/SoftwareDevelopmentPractices.pdf).

# Overview
CICE consists of a top level driver and dynamical core plus the Icepack code which is included as a git submodule.  Because Icepack is a submodule of CICE, Icepack and CICE development are handled somewhat independently with respect to the github repositories even though development and testing may be done together and in the same sandbox.  

Only a limited number of users are able to push to the CICE-Consortium repositories.  Users will be working on personal forks and executing pull requests to merge their fork to the CICE-Consortium repositories.  If you plan to work within the CICE-Consortium project, create a github account (https://github.com) if you don’t have one already.

A good tutorial on the overall git workflow is at atlassian's comparing-workflows page.  We will be following most of the ideas discussed in those workflows.  Details about using git can be found at the git-scm site or use google search.

There are a few basics to understand about git.  It is distributed.  That means there are actually multiple repositories.  For instance, normally there will be the CICE-Consortium repository, a user’s forked repository, and a local repository on your local machine associated with your sandbox.  The sandbox just contains a particular version from your repository like the head of a specific branch.  The sandbox is where you work.  To download a copy of the repository to a local file system, you clone it in git, that creates the local repository and sets up the sandbox.  That sandbox will be set to the head of the master branch initially.  You can update your local repository from any other repository by using fetch and merge (aka pull).  When you commit, you are migrating changes from your sandbox to your local repository.  Use push to migrate changes in the local repository back to your fork.  Once your fork is ready, those changes will be migrated to the CICE-Consortium repository by executing a pull request.   To update your local sandbox, you execute a pull from a github repository.  More generally, you can pull or push from/to any github repository.

# Local Initialization
Before using git on any platform, it’s useful to set a few things.  Execute the following commands,

      git config --global user.name "Your Github Username"
      git config --global user.email you@yourdomain.com
      git config --global push.default simple[a]

You only need to set these once for each independent platform, they will be stored in the file ~/.gitconfig

# Forks
## Setting Up Forks


Users should create personal forks of CICE and Icepack to carry out any development of the CICE or Icepack source code.  To create a fork (you do this once), 
* Go to the repository page (ie. https://github.com/CICE-Consortium/CICE or https://github.com/CICE-Consortium/Icepack)
* In the upper right hand corner, click on “fork”
* Click on your github avatar/username
* A fork will be created on your github page (ie. https://github.com/username/CICE)

Each repository (CICE and Icepack) have to be forked separately and users are encouraged to fork both repositories.


We encourage development on branches in forks and for the fork master to generally remain up to date with the Consortium version.  This makes it easier to branch in the fork from a Consortium version of master.

## Updating Your Fork

We’re getting a little ahead with respect to documentation but to update your fork from an upstream source, pull from the CICE-Consortium (or another repository) to your local sandbox, commit locally, and then push those changes to your fork.  Typically, this looks like

      git clone https://github.com/username/CICE --recursive
      cd CICE
      git remote -v
      git remote add upstream https://github.com/CICE-Consortium/CICE
      git remote -v
      git pull upstream master
      git push origin master

This entire process clones your fork which creates a local repo and sandbox, pulls changes from the CICE-Consortium (ie. upstream) master into your local sandbox, commits those changes to your local repository, and pushes those changes to your fork (origin).  The process above is how you can keep your fork master up-to-date with the Consortium master.  Whatever branch the sandbox is pointing to is the branch that will be updated by the pull.

## Collaborators

In general, your forks are public, anyone can read, but nobody can write.  You can add collaborators to your fork by logging into github and going to the repository, e.g. https://github.com/username/cice, clicking on Settings, then Collaborators.  Then add the collaborator at the bottom of the page.  When you do, that person will be invited to collaborate on your fork and you can give them write permission.

# Clone, Commit, Branch
## Creating a Sandbox (clone)
To create the initial sandbox, use git clone.

      git clone https://github.com/username/CICE --recursive

--recursive populates all submodules, which is useful for CICE since Icepack is a submodule.  If you forget to use --recursive then

      git clone https://github.com/username/CICE
      cd CICE
      git submodule update --init

When you clone, your sandbox will be set to the head of the master branch.  You can also specify a local directory name with git clone 

      git clone https://github.com/username/CICE --recursive mysandbox

to name the cloned sandbox. Verify with git status.

      git status
        On branch master
        Your branch is up-to-date with 'origin/master'.
        nothing to commit, working directory clean

To clone a branch from someone else’s fork,

      git clone -b branch_name --recursive https://github.com/username/CICE mybox

## Commit

When you commit, you are committing changes to the local repository.  This repository is part of your sandbox and is created when you clone.  In general, you want to use git status, git add, git rm, and git commit.  Git status indicates where you are in the repository and what changes have been made in your sandbox.  Git add tells git which files you want to update in the local repository when you commit.  Git commit then commits those to your local repository.  

      git status
      git add file1
      git add file2 file3
      git add file4
      git commit -m “modified this really cool thing in my code”
      git status

## Branch

Branches and forks are often treated the same, but they are fundamentally different. A fork is a copy of an entire repository; that repository contains branches. A branch is a specific version in a repository.

To see which branches exist, use,

      git branch --list
      git branch --list --all

--all shows all remote branches.  To switch to an existing branch, use git checkout.

      git checkout branchname

You can also checkout a branch directly with clone using the -b option,

      git clone -b branchname https://github.com/username/CICE --recursive

To create a new branch, set your sandbox to point where you want to create a branch and use git branch to create it, then checkout that branch to switch to it,

      git checkout master
      git branch newbranch
      git checkout newbranch

We recommend that you give your branches meaningful names, because you likely will create and use many of them, and this helps identify pull requests.  E.g. for a bug fix, you might use something like “bugfix_thermo_conductivity.”  We recommend you work only on branches in your fork and that master is consistent with the CICE-Consortium repository to have a stable version to create branches from.  To update your fork master to the latest Consortium version, see this section on remote/pull/push.  **NOTE: When you execute “git checkout”, you will switch branches and lose any local modifications that have not been committed so BE CAREFUL with checkout.** Commit and push any changes before you switch branches.  You can also use “git stash” to save local changes.

If you are working on a branch[b][c][d][e][f][g][h], when you commit, you want to commit only the changes on the branch, and then you’ll want to push the branch changes to the repository.

      git status
         On branch newbranch
         Your branch is up-to-date with 'origin/newbranch'.
         Changes not staged for commit:
         ... 
      git add file1 file2
      git commit -m “updated the big subroutine to fix the little algorithm”
      git push origin newbranch

To delete a branch

      git checkout master
      git branch -d newbranch

If you are going to checkout a branch with a submodule,  

* You can clone the branch directly,

      git clone -b branchname --recursive https://github.com/username/CICE 

* You can clone the repository without --recursive, switch to the branch, and then init and update the submodule,

      git clone https://github.com/username/CICE 
      cd CICE
      git checkout branchname
      git submodule update --init

* If you already have a sandbox with the submodule initialized, you need to sync and update the submodule after you switch branches if the origin of the submodule has changed,

      cd CICE
      git checkout branchname
      git submodule sync
      git submodule update --init

# Pushing and Pulling

Pushing and Pulling are operations associated with migrating changes between repositories.  You push something if you are acting on the “sending” side and you pull something if you are on the “receiving” side.  To push or pull, you have to identify the repository and what you want to migrate, and you need write access to that repository.  The git remote command is extremely useful in push and pull operations.

## Remotes

      git remote -v
         origin    https://github.com/username/CICE (fetch)
         origin    https://github.com/username/CICE (push)

shows the repositories that are currently associated with your local repository.  By default, the repository that was cloned will be “origin”.  Others can be added easily, e.g.,

      git remote add upstream https://github.com/CICE-Consortium/CICE
      git remote add buddy https://github.com/anotherusername/CICE
      git remote -v
         buddy    https://github.com/anotherusername/CICE (fetch)
         buddy    https://github.com/anotherusername/CICE (push)
         origin    https://github.com/username/CICE (fetch)
         origin    https://github.com/username/CICE (push)
         upstream    https://github.com/CICE-Consortium/CICE (fetch)
         upstream    https://github.com/CICE-Consortium/CICE (push)

Now you can pull or push from/to these repositories.  

## Push

A typical workflow for development with push would be

      git clone https://github.com/username/CICE
      cd CICE
      git checkout master
      git branch mybranch
      git checkout mybranch
         develop and test
      git status
      git add <file1      <file2     
      git commit -m “developed and tested on mybranch”
      git push origin mybranch

## Pull

If you want to update your master fork with changes from the CICE-Consortium master, you would pull from the master and push to your fork as follows

      git checkout master
      git remote add upstream https://github.com/CICE-Consortium/CICE
      git pull upstream master (pulls upstream repo master to local repo, sandbox)
      git push origin master (pushes your local repo master to your fork)

To then update your branch to the latest changes on the master, you would do

      git checkout mybranch
      git pull origin master (merge updates from fork/origin master to mybranch)
  test
      git add    (if any local changes were made)
      git commit  (if any local changes were made)
      git push origin mybranch      

A pull is the same thing as a fetch and a merge.  There are many cases where it’s better to do a fetch, review the changes (git diff), and then do a merge.  So

      git pull origin master

Is the same as

      git fetch origin
      git merge origin/master

# Pull Requests (PR)

All modifications to the CICE-Consortium repositories will have to be done via a pull request from a fork.  These pull requests will be formally reviewed and tested before being accepted and pulled into the Consortium repository.  In general, the recommended process is to create a branch in a fork, develop and test, keep up to date with the CICE-Consortium master, document, and then when ready execute a pull request to the Consortium repository.

To execute a pull request, 
* Login to your fork in github (i.e. https://github.com/username/CICE)
* Click on the appropriate repository
* Switch to the appropriate branch via the drop down box
* Click on the box “New Pull Request” next to the branch name
* Review and verify the changes
* Review and verify that the base and head are accurate
* Add any relevant documentation and propose reviewers
* Click on the “create pull request” box

# Submodules

## Overview

Icepack is a submodule of CICE.  Submodules are pointers to specific versions of an external repository.  Working with Icepack in CICE is like working with a repository in a repository.  If you are working in the Icepack repository in stand-alone mode, you can ignore this and follow the documentation above.  But there are a few extra steps if you are modifying Icepack in the CICE code.

## Modify Icepack Code Inside CICE

When Icepack is downloaded as part of CICE, the Icepack version will be a detached HEAD.  Without going into too much detail, that means it’s not in a state where it can be modified and committed.  It’s pointing to a specific version of Icepack, not to a branch.

      cd icepack
      git remote -v
         origin    https://github.com/CICE-Consortium/Icepack (fetch)
         origin    https://github.com/CICE-Consortium/Icepack (push)
      git status
         HEAD detached at 192fbaa
         nothing to commit, working directory clean

Icepack is pointing to something in the CICE-Consortium Repository, even if you checked Icepack out of your fork.  If you need to modify Icepack, the first thing to do is to switch the Icepack submodule to the head of a branch in your fork.  To do this, you need to modify the submodule repository, update the submodule version to your fork master, update the fork master to make sure you are using the latest version of the Consortium Icepack code, then switch to a branch in your fork.  Make sure your fork master is up to date with the Consortium master and if not, [update your fork](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_edit#updating-your-fork).

      cd CICE
      git config --file=.gitmodules -l
      git config --file=.gitmodules submodule.icepack.url https://github.com/username/Icepack.git
      git config --file=.gitmodules submodule.icepack.branch master
      git config --file=.gitmodules -l
      git submodule sync
      git submodule update --init  
      cd icepack
      git remote -v
         origin    https://github.com/username/Icepack.git (fetch)
         origin    https://github.com/username/Icepack.git (push)
      git status
         HEAD detached at 903678f
         nothing to commit, working directory clean
      git checkout master  (switch from the detached HEAD to your fork master)
      git remote add upstream https://github.com/CICE-Consortium/Icepack
      git merge upstream master
      git push origin master
      git branch testmods1
      git checkout testmods1
      git status
         On branch testmods1
         nothing to commit, working directory clean

## Modify and Commit Icepack Changes

Now you are ready to modify the Icepack code, commit Icepack locally, and push your branch changes to your Icepack fork.  This is just like working in any git repository.

         Modify Icepack code, test, and review
      cd icepack
      git status
      git diff
      git add file1
      git commit -m “update something really special in a nice way”
      git push origin testmods1

When ready, execute a pull request from your Icepack fork to the CICE-Consortium repository.  When the pull request is executed, your Icepack changes will be merged into the CICE-Consortium version.
## Update the Icepack Version in CICE
However, CICE is still pointing to the older version of Icepack in all repositories.  To update the CICE submodule version[i][j], you just need to switch Icepack to the version of code of interest and then commit the submodule change to CICE.  For instance

      git branch cicebranch
      git checkout cicebranch
      cd icepack
      git status
      git branch -a
      git checkout somebranch
      cd .. 
      git status
      git add icepack  (add Icepack changes to CICE)
      git commit  (in CICE)
      git push origin cicebranch

The exact commands and sequence will vary a bit depending what you want to do.  This will have to be done regularly in the CICE-Consortium version to keep Icepack up to date.  In general, the Icepack submodule may not need to be formally updated until a pull request is done.  In most cases, it should be fine to develop, commit, and push on a fork branch in both CICE and Icepack at the same time without ever fussing with submodules.  A process for working on CICE and Icepack at the same time is

1.  clone CICE from user fork
1.  update CICE fork master to Consortium version
1.  create and checkout a CICE fork branch
1.  switch Icepack to user fork
1.  update Icepack fork master to Consortium version
1.  create and checkout Icepack fork branch
1.  develop/commit/push Icepack changes to Icepack fork branch, develop/commit/push CICE changes to CICE fork branch, never update CICE submodule formally in fork branch
1.  execute PR for Icepack to merge changes to Consortium Icepack master
1.  update CICE fork branch submodule to point to the appropriate Consortium Icepack version and commit/push that change to the CICE fork branch
1.  execute PR for CICE to merge changes to Consortium CICE master including updating the pointer to the Icepack version

By using this approach, only at the final CICE commit is the Icepack submodule updated.  There may be times where this is not adequate, but as a default, it’s probably the easiest way to carry out development of Icepack and CICE in parallel.

## Completely Remove and Replace the Icepack Submodule in CICE

This is not something you should normally have to do, but just in case,

      cd CICE
      git submodule deinit -f icepack
      rm -r -f .git/modules/icepack
      git rm -f icepack
      git commit -m “remove icepack”
      git submodule add https://github.com/username/Icepack icepack
      cd icepack
      git checkout some_branch
      cd ../
      git add icepack
      git commit -m “switch to Icepack repo from username”

and now you can push the change to CICE.  

# Information

There are many git commands to understand the status of your sandbox.

## Status
Status provides a summary of the status of your sandbox.  

      git status

will indicate which branch your sandbox is on and the changes that have been made.  This should be used often before commits and pushes.

## Diff
Diff shows code changes.

      git diff
## Log
Log summarizes the commits and pushes in your sandbox up to the current state.  The first entry will provide the id of the current model version.

      git log

If you want a useful graphical summary of the log, try

      git log --graph --oneline --decorate


***

# Appendix A: Table of Useful git Commands  (git [command])

 | [command] | Description |
 | --------- | ----------- |
 | status    | Provides summary of status of sandbox |
 | diff    | Provides list of changes in current sandbox, lots of options for doing diffs with other repo versions.|
 | remote [-v] [add] | 	Lists/Sets remote repositories in a sandbox |
 | pull | Download changes to local sandbox (== fetch + merge) |
 | push | Upload changes |
 | clone | Initialize a local repo/sandbox |
 | update | Pull updates into the local sandbox |
 | commit | Copy changes into the local sandbox repository |
 | submodule | 	Many options, useful for working with submodules |
 | checkout | Switch to another version/branch |
 | branch | Create a branch or list branches |
 | tag -a | Create a tag or list tags |
 | log | Provide a summary of commits |
 | add | Defines which files will be committed |
 | rm | Removes a file from the repo |
 | fetch | Download changes to local repo |
 | merge | Merge changes from local repo to sandbox |
 | pull request | A request to merge changes from one repo to another.  AKA PR. |

# Appendix B: Best Practices
* Create a fresh clone and branch for each batch of changes that will be submitted in separate PRs, if a previous PR might not be executed before work begins on the next one.
* Update your fork from the main Consortium repositories. 
* Always develop on a branch, then later merge (or pull request) to master.
* Use “git status” often.
* Use “git remote -v” often.
* Always commit with a reasonably detailed and clear commit message.

# Appendix C: Terms
_Branch_ - A pointer to a parallel development in a repository    
_Checkout_ - When you switch to a branch in your local repository    
_Commit_ - When you copy changes into your local repository    
_Clone_ - When you copy a github repository into a local sandbox    
_Fetch_ - When you update your local repository from an external repository    
_Fork_ - When you copy a repository within github from one github project to another    
_Master_ - The main or trunk branch in a github repository    
_Merge_ - Merging changes from your local repository to your sandbox    
_Pull_ - When you copy changes out of an external repository to your local repository and merge those changes into your local sandbox.  This is a combination of fetch and merge    
_Pull Request_ - A github operation to request an update to an upstream repository    
_Push_ - When you copy changes into a github repository    
_Sandbox_ - Your local checkout with or without local modifications    
_Submodule_ - An external repository included in another repository    
_Tag_ - The ability to explicitly name a specific version of the module in a repository    

