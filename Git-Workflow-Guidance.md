# Table of Contents
[**Introduction**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#introduction)  
[**General Recommendations**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance#general-recommendations)    
[**Overview**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#overview)   
[**Local Initialization**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#local-initialization)   
[**Forks**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#forks)   
* Setting up Forks    
* Updating your Fork Master
* Collaborators    

[**Clone, Commit, Branch**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#clone-commit-branch)   
* Creating a Sandbox (clone)    
* Branch   
* Commit    
 

[**Pushing and Pulling**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#pushing-and-pulling)   
* Remotes    
* Push    
* Pull  

[**Pull Requests (PR)**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#pull-requests)
* Overview
* Refreshing your PR

[**Overall Workflow**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#overall-workflow)

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

## General Recommendations
* _Create your own forks for each repository._

* Keep your fork master consistent with the Consortium master:
_pull from the Consortium master and push to your fork master_  

* Work on branches in your sandbox, not on master.
Always branch from master unless you specifically want changes from another branch in the new branch.
Use different sandboxes for different branches.
_Never push changes to your fork master, only to branches._

* _Before a Pull Request, [update your fork](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance#updating-your-fork-master) using the Consortium master as your upstream source._

* _Before a Pull Request run the appropriate tests (see [Resource Guide](https://github.com/CICE-Consortium/About-Us/wiki/Resource-Index#model-testing) for details) and include test information in the PR template._

* _Separate updates into multiple Pull Requests (one "fix" at a time)._ Fill in the Pull Request template with details specific to each particular "fix". This is especially important if some changes are bit-for-bit and others are not. 

* Be very careful with every pull and push command to make sure it's from/to the right repo/fork/branch and contains what is intended.  
_Use ‘git status’ and ‘git remote -v’ frequently._

See also our [Software Development Practices](https://github.com/CICE-Consortium/About-Us/wiki/Software-Development-Practices).

## Overview
CICE consists of a top level driver and dynamical core plus the Icepack code which is included as a git submodule.  Because Icepack is a submodule of CICE, Icepack and CICE development are handled somewhat independently with respect to the github repositories even though development and testing may be done together and in the same sandbox.  

Only a limited number of users are able to push to the CICE-Consortium repositories.  Users will be working on personal forks and executing pull requests to merge their changes into the CICE-Consortium repositories.  If you plan to work within the CICE-Consortium project, create a github account (https://github.com) if you don’t have one already.

A good tutorial on the overall git workflow is at [atlassian's comparing-workflows page](https://www.atlassian.com/git/tutorials/comparing-workflows).  We will be following most of the ideas discussed in those workflows.  Details about using git can be found at the git-scm site or use google search.

There are a few basics to understand about git.  It is distributed.  That means there are actually multiple repositories.  For instance, normally there will be the github CICE-Consortium repository, a user’s github forked repository, and a local repository on your local machine associated with your sandbox.  The sandbox just contains a particular version from your repository like the head of a specific branch.  The sandbox is where you work.  To download a copy of the repository to a local file system, you clone it in git, that creates the local repository and sets up the sandbox.  That sandbox will be set to the head of the master branch initially and will contain all branches and tags from the remote repository at the time of the clone.  You can update your local repository from any other repository by using fetch and merge (aka pull).  When you commit, you are migrating changes from your sandbox to your local repository.  Use push to migrate changes in the local repository back to your fork.  Once your fork is ready, those changes will be migrated to the CICE-Consortium repository by executing a pull request.   To update your local sandbox, you execute a pull from a github repository.  More generally, you can pull or push from/to any github repository.

<!---
![repodiagram](https://github.com/CICE-Consortium/About-Us/wiki/images/CICE_repo_diagrams1.png)
-->

<img src="https://github.com/CICE-Consortium/About-Us/wiki/images/CICE_repo_diagrams1.png" width="500" title="repodiagram">

_**Figure: Relationship between CICE consortium repositories and git commands**_

# Getting Started with GIT

## Setup a Github account

You can clone (checkout) the CICE-Consortium code without a Github account, but if you want to have your own repository and contribute, you'll need a Github account.  To setup a Github account, go to [github.com](https://github.com) and click on the SignUp button in the upper right hand side.

Thereafter, you will SignIn when you go to github.com.

## Local Initialization
Before using git on any platform, it’s useful to set a few things.  Execute the following commands,

      git config --global user.name "Your Github Username"
      git config --global user.email you@yourdomain.com
      git config --global push.default simple

You only need to set these once for each independent platform, they will be stored in the file ~/.gitconfig

## Setting Up Forks


Users should create personal forks of CICE and Icepack to carry out any development of the CICE or Icepack source code.  To create a fork (you do this once), 
* Go to the repository page (ie. https://github.com/CICE-Consortium/CICE or https://github.com/CICE-Consortium/Icepack)
* In the upper right hand corner, click on “fork”
* Click on your github avatar/username
* A fork will be created on your github page (ie. https:// github.com/username/CICE)

Each repository (CICE and Icepack) have to be forked separately and users are encouraged to fork both repositories.


We encourage development on branches in forks and for the fork master to generally remain up to date with the Consortium version.  This makes it easier to branch in the fork from a Consortium version of master.

## Updating Your Fork master

We’re getting a little ahead with respect to documentation but to keep your fork master up to date with the consortium master, pull from the CICE-Consortium to your local sandbox, commit locally, and then push those changes to your fork.  Typically, this looks like

      git clone https://github.com/username/CICE --recursive  # first-time only
      cd CICE
      git remote add upstream https://github.com/CICE-Consortium/CICE  # first-time only
      git pull upstream master
      git submodule update
      git push origin master

This entire process clones your fork master which creates a local repo and sandbox, pulls changes from the CICE-Consortium (ie. upstream) master into your local sandbox and commits those changes to your local repository, and pushes those changes to your fork (origin).  We encourage all users to NOT commit local changes to master (always work on a branch), and to keep the fork master up to date with the consortium master.

## Collaborators

In general, your forks are public, anyone can read, but nobody can write.  You can add collaborators to your fork by logging into github and going to the repository, e.g. https:// github.com/username/cice, clicking on Settings, then Collaborators.  Then add the collaborator at the bottom of the page.  When you do, that person will be invited to collaborate on your fork and you can give them write permission.

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

Verify with git status and git remote -v

      git status
        On branch master
        Your branch is up-to-date with 'origin/master'.
        nothing to commit, working directory clean

      git remote -v
        origin	https://github.com/username/CICE (fetch)
        origin	https://github.com/username/CICE (push)


You can clone any public github repository.

## Branch

Branches and forks are often treated the same, but they are fundamentally different. A fork is a copy of an entire repository; that repository contains branches. A branch is a specific version in a repository.

To see which branches exist, in a sandbox,

      git branch --list
      git branch --list --all

--all shows all remote branches.  To switch to an existing branch, use `git checkout`, then `git submodule update`.

      git checkout branchname
      git submodule update  # needed to synchronize your Icepack checkout.
      # or, do both in one command :
      git checkout --recurse-submodules branchname

You can also checkout a branch directly with clone using the -b option from any github location,

      git clone -b branchname https://github.com/username/CICE --recursive

To create a new branch, initialize your sandbox to the version you want to branch from and type,

      git branch mybranch

You will usually branch from the head of the consortium master, and this is good time to update your fork's master as part of the process,

      git clone https://github.com/username/CICE --recursive cice.mybranch
      cd cice.mybranch
      git remote add upstream https://github.com/cice-consortium/CICE
      git pull upstream master
      git submodule update
      git push origin master
      git branch mybranch
      git checkout mybranch

The first 6 lines above just update master in your fork with the consortium version.  Then the branch is created from the head of master and it is checked out.  

We recommend that you give your branches meaningful names, because you likely will create and use many of them, and this helps identify pull requests.  E.g. for a bug fix, you might use something like “bugfix_thermo_conductivity.”  We recommend you work only on branches in your fork and that master is consistent with the CICE-Consortium repository to have a stable version to create branches from.  **NOTE: When you execute “git checkout”, you will switch branches and lose any local modifications that have not been committed so BE CAREFUL with checkout.** Commit and push any changes before you switch branches.  You can also use “git stash” to save local changes.

To delete a branch

      git checkout master
      git branch -d newbranch

If your branch has a submodule (all CICE branches should since Icepack is a submodule!), 

* You can create the branch as part of the clone,

      git clone -b branchname --recursive https://github.com/username/CICE 

* You can clone the repository without --recursive, switch to the branch, and then init and update the submodule,

      git clone https://github.com/username/CICE 
      cd CICE
      git checkout branchname
      git submodule update --init

* Or if you already have a sandbox with the submodule initialized, you can switch to the branch and then you should sync and update/init the submodule,

      git clone --recursive https://github.com/username/CICE
      cd CICE
      git checkout branchname
      git submodule sync
      git submodule update --init


## Commit

When you commit, you are committing changes to the local repository.  This repository is part of your sandbox and is created when you clone.  In general, you want to use git status, git add, git rm, and git commit.  Git status indicates where you are in the repository and what changes have been made in your sandbox.  Git add tells git which files you want to update in the local repository when you commit.  Git commit then commits those to your local repository.  

      git status
      git add file1
      git add file2 file3
      git add file4
      git rm file5
      git commit -m “modified this really cool thing in my code”
      git status

In this case, add specifies both new AND modified files that need to be committed.  You can also use `git commit -a` to automatically add modified files, but please review the git documentation first.

# Pushing and Pulling

Pushing and Pulling are operations associated with migrating changes between repositories.  You push something if you are acting on the “sending” side and you pull something if you are on the “receiving” side.  To push or pull, you should specify the repository and what is being migrated explicitly, and you will need write access to that repository.  The git remote command is extremely useful in push and pull operations.

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

Push migrates changes from your local repository TO the github repository.  Push looks like

      git push origin mybranch

You push to the repository of interest (ie. origin) and on the branch of interest (ie. mybranch).

## Pull, Rebase

If you want to update your master fork with changes from the CICE-Consortium master, you would pull from the consortium and push to your fork as follows

      git checkout master
      git remote add upstream https://github.com/CICE-Consortium/CICE
      git pull upstream master      # pulls upstream repo master to local repo and sandbox
      git submodule update          # updates your Icepack submodule sandbox to the version you just pulled
      git push origin master        # pushes your local repo master to your fork

A similar process can be used to update a branch.  However, on a branch, we recommend using rebase rather than pull.  Pull merges upstream and local changes based on time of commit.  Rebase updates the local repository by first rebasing the repository from the upstream source and then replaying your local commits on top of the rebase.  That means your local changes are always built on top of the base.  This would look like

      git checkout branchname
      git remote add upstream https://github.com/CICE-Consortium/CICE
      git pull --rebase upstream master
      git submodule update
      git push origin branchname

This works fine if your push is just a fast-forward push.  If you have pushed the branch before the rebase, it probably won't be a fast-forward as the history of your local repo and the remote repo have diverged.  To overcome this, you'll have to do one of two things.  Either force the push and overwrite the history on your branch in your repo.  This is perfectly fine if nobody else is working in your branch.  That would look like

      git push --force-with-lease origin branchname

The force-with-lease (versus just force) checks whether you might overwrite other commits on your branch before forcing.  The other option is to work on a new branch and pull changes from the old branch to the new branch.  Neither are ideal.  
Pull and rebase can result in conflicts.  If there are conflicts, they will be reported and you will have to fix them to continue.  With pull, you will have to resolve the conflicts and commit manually.  With rebase, you will have to resolve the conflicts and use git rebase --continue.  See the git documentation for more details about handling conflicts.  In summary, to rebase a branch with conflicts, do the following

      git clone https://github.com/username/CICE --recursive
      git checkout branchname
      git remote add upstream https://github.com/CICE-Consortium/CICE
      git fetch upstream master
      git rebase upstream/master
      > hand edit conflicts
      git rebase --continue
      git submodule update
      git push --force-with-least origin branchname

Your branch will now be rebased to the current master and your pull request should update and reflect that.


A pull is the same thing as a fetch and a merge.  There are many cases where it’s better to do a fetch, review the changes (git diff), and then do a merge.  So

      git pull origin master

Is the same as

      git fetch origin
      git merge origin/master

# Pull Requests

## Overview

All modifications to the CICE-Consortium repositories will have to be done via a Pull Request (PR) from a fork.  These pull requests will be formally reviewed and tested before being accepted and pulled into the Consortium repository.  In general, the recommended process is to create a branch in a fork, develop and test, keep up to date with the CICE-Consortium master, document, and then when ready execute a pull request to the Consortium repository.

To execute a pull request, 
* Login to your fork in github (i.e. https:// github.com/username)
* Click on the appropriate repository
* Switch to the appropriate branch via the drop down box
* Click on the box “New Pull Request” next to the branch name
* Review and verify the changes
* Review and verify that the base and head are accurate
* Add any relevant documentation in the template box and propose reviewers
* Click on the “create pull request” box

## Refreshing your PR

There are times where a PR is conflicting with the destination code, where the PR shows changes related to pulls from master, where the PR isn't running correctly, or where the PR just is not reviewable or readable for various reasons.  One option is to delete the PR and create a new one.  The easiest way is to create a new branch off the current master and pull from the old branch.  Lets assume the current branch is called feature.  These steps (or similar) should allow you to continue fairly quickly

     git clone https://github.com/user/cice cice.feature2
     cd cice.feature2
     git remote add upstream https://github.com/cice-consortium/cice
     git pull upstream master
     git submodule update
     git push origin master
     git branch feature2
     git checkout feature2
     git pull origin feature
       (review and test)
     git add ...
     git commit -m "pull feature branch to feature2 branch"
     git push origin feature2
     (delete pull request for feature branch)
     (create pull request for feature2 branch)

# Overall Workflow

To summarize, a typical workflow for development on a branch would be

      git clone https://github.com/username/CICE cice.mybranch --recursive
      cd cice.mybranch
      git remote add upstream https://github.com/cice-consortium/CICE
      git pull upstream master
      git submodule update
      git push origin master
      git branch mybranch
      git checkout mybranch
         (develop and test)
      git status
      git add file1 file2     
      git rm file3
      git commit -m “developed something and tested on mybranch”
         (develop and test)
      git add file4
      git commit -m "updated something again"
      git rebase upstream master
         (test)
      git commit -m "rebase to master"
      git push origin mybranch
      (create the Pull Request)


# Submodules

## Overview

Icepack is a submodule of CICE.  Submodules are pointers to specific versions in an external repository.  Working with Icepack in CICE is like working with a repository in a repository.  When Icepack is downloaded as part of CICE, the Icepack version will be a detached HEAD and probably associated with a version in the consortium repository, even if you checked out a version of CICE from your fork.  Without going into too much detail, a detached HEAD means it’s not in a state where it can be modified or committed.  

      git clone https://github.com/username/cice --recursive
      cd cice/icepack
      git remote -v
         origin    https://github.com/CICE-Consortium/Icepack (fetch)
         origin    https://github.com/CICE-Consortium/Icepack (push)
      git status
         HEAD detached at 192fbaa
         nothing to commit, working directory clean

## Update Icepack in CICE

If all you want to do is change the Icepack version in CICE in the repository, then you would do the following

      git clone https://github.com/username/CICE cice.mybranch --recursive
      cd cice.mybranch
      (update to Consortium CICE master if needed)
      git branch mybranch
      git checkout mybranch
      cd icepack
      git status                # should be in a detached HEAD
      git branch --all --list   # figure out what to checkout
      git checkout somebranch   # checkout a new version of Icepack from the consortium
      git status                # should be pointing to another version of Icepack
      cd .. 
      (test CICE)
      git add icepack           # add Icepack changes to CICE
      git commit                # in CICE
      git push origin mybranch
      (create PR for CICE)

## Keep Icepack up-to-date when pulling CICE from the Consortium master
As indicated [above](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/#pull-rebase), you need to update the Icepack submodule using 
```bash
git submodule update
```
after you pull from the Consortium CICE master. This is because Git will fetch submodule changes automatically when doing `git pull` but it will **not** update your local submodule working directory.  
It might also be necessary to run `git submodule update` after switching branches if the branches record the Icepack submodule at different commits.

## Develop CICE and Icepack concurrently

There are a number of different ways to handle development of Icepack and CICE concurrently.  The easiest way is probably to checkout CICE and Icepack from your fork, and develop each within a single sandbox but as independent branches.  Then do a PR for Icepack first, and finally update Icepack in CICE in your fork and do a CICE PR.  This process looks like

1.  clone CICE from user fork
1.  update CICE fork master to Consortium version
1.  create and checkout a CICE fork branch
1.  clone Icepack to user fork
1.  update Icepack fork master to Consortium version
1.  create and checkout Icepack fork branch
1.  develop/commit/push Icepack changes to Icepack fork branch, develop/commit/push CICE changes to CICE fork branch, never update CICE submodule formally in fork branch
1.  execute PR for Icepack to merge changes to Consortium Icepack master
1.  update CICE fork branch submodule to point to the appropriate Consortium Icepack version and commit/push that change to the CICE fork branch
1.  execute PR for CICE to merge changes to Consortium CICE master including updating the pointer to the Icepack version

By using this approach, only at the final CICE commit is the Icepack submodule updated.  There may be times where this is not adequate, but as a default, it’s probably the easiest way to carry out development of Icepack and CICE in parallel.  More specifically, this might look something like

      git clone https://github.com/username/CICE cice.mybranch --recursive
      cd cice.mybranch
      (update to Consortium CICE master if needed)
      git branch mybranch
      git checkout mybranch
      mv icepack icepack.orig                                  # put aside the original version of icepack
      git clone https://github.com/username/icepack icepack    # check out a new version of icepack from your fork and drop it into your icepack directory in your sandbox
      cd icepack
      (update to Consortium Icepack master if needed)
      git branch icebranch
      git checkout icebranch
      (modify icepack and cice, test icepack and cice, add/commit/push icepack and cice, as separate repositories)
      git push origin icebranch                                # push all changes to Icepack repository
      (create a PR for icebranch and wait for the Icepack PR to be done)

      cd cice.mybranch
      git push origin mybranch                                 # push all changes to CICE repository
      mv icepack icepack.new                                   # put aside your working copy of icepack
      git clone https://github.com/cice-consortium/icepack icepack      # check out the consortium icepack master
      diff -r icepack icepack.new                              # just make sure it looks OK
      (test CICE)
      git add icepack
      git commit -m "update icepack version"
      git push origin mybranch
      (create a PR for CICE that will include CICE mods and a new version of Icepack)

You just need to be a little careful to keep track of the Icepack and CICE changes separately.

## Change the Icepack submodule in CICE

This is more advanced, but you can also change the submodule that Icepack is pointing to within a CICE repository.  To do this, you need to modify the submodule repository, update the submodule version using git config, then commit and push the change.  

      git clone https://github.com/username/CICE cice.mybranch --recursive
      cd cice.mybranch
      (update to Consortium CICE master if needed)
      git branch mybranch
      git checkout mybranch   # work on CICE branch
      git config --file=.gitmodules -l
      git config --file=.gitmodules submodule.icepack.url https://github.com/username/Icepack.git  # change the repository
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
      git checkout something   # change the version of Icepack
      cd ../
      git add icepack
      git commit -m "switch icepack to different repository"

This should be avoided as it just means that later on, you will have to change the Icepack repository back to a version in the consortium if you want to PR this CICE branch.  It's far easier to just treat the Icepack repository independently until you are ready to checkout a new version from the consortium to update CICE.

## Completely Remove and Replace the Icepack Submodule in CICE

This is not something you should normally have to do, but just in case,

      cd CICE
      git submodule deinit -f icepack
      rm -r -f .git/modules/icepack
      git rm -f icepack
      git commit -m “remove icepack”
      git submodule add https://github.com/cice-consortium/Icepack icepack
      cd icepack
      git checkout some_branch
      cd ../
      git add icepack
      git commit -m “switch to Icepack version xyz”

and now you can push the change to CICE.  

# Information

There are many git commands to diagnose the status of your sandbox.

## Status
Status provides a summary of the status of your sandbox.  

      git status

will indicate which branch your sandbox is on and the changes that have been made.  This should be used often during development and before commits and pushes.

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
 | add | Defines which files will be committed |
 | branch | Create a branch or list branches |
 | checkout | Switch to another version/branch |
 | clone | Initialize a local repo/sandbox |
 | commit | Copy changes into the local sandbox repository |
 | diff    | Provides list of changes in current sandbox, lots of options for doing diffs with other repo versions.|
 | fetch | Download changes to local repo |
 | log | Provide a summary of commits |
 | merge | Merge changes from local repo to sandbox |
 | pull | Download changes to local sandbox (== fetch + merge) |
 | push | Upload changes |
 | rebase | like pull but updates the base version then replays local changes |
 | remote [-v] [add] | 	Lists/Sets remote repositories in a sandbox |
 | rm | Removes a file from the repo |
 | status    | Provides summary of status of sandbox |
 | submodule | 	Many options, useful for working with submodules |
 | tag -a | Create a tag or list tags |
 | update | Pull updates into the local sandbox |

# Appendix B: Best Practices
* Create a fresh clone and branch for each batch of changes that will be submitted in separate PRs, if a previous PR might not be executed before work begins on the next one.
* Keep your fork master up to date with the Consortium, don't commit local changes to your fork master, and rebase your branches from the main Consortium repositories periodically. 
* Always develop on a branch, then create a PR to merge to the consortium master.
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
_Pull Request_ - A github operation to request an update to an upstream repository (aka PR)    
_Push_ - When you copy changes into a github repository    
_Sandbox_ - Your local checkout with or without local modifications    
_Submodule_ - An external repository included in another repository    
_Tag_ - The ability to explicitly name a specific version of the module in a repository    

