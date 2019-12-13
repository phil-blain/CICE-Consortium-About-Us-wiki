# Table of Contents
[**Introduction**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#introduction) 
* General Recommendations
* Git Overview

[**Getting Started with Git**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#getting-started-with-git) 
* Setup a Github Account
* Local Git Initialization
* Setting up Github Forks
* Updating your Github Fork Master
* Git Collaborators

[**Clone, Commit, Branch**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#clone-commit-branch)   
* Clone
* Branch
* Commit
 

[**Pushing and Pulling**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#pushing-and-pulling)   
* Remotes
* Push
* Pull, Rebase
* Some examples
  * Update fork master from Consortium master
  * Update a branch from Consortium master
  * Rejected pushes
  * Push to a different repository

[**Pull Request (PR)**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#pull-request)
* PR Overview
* Refreshing your PR

[**Submodules**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#submodules)   
* Submodule Overview
* Update Icepack in CICE
* Resync Icepack in CICE
* Development of Icepack under CICE
* Develop Icepack and CICE Concurrently
* Switch the Icepack Submodule Repository
* Remove and Replace the Icepack Submodule

[**Final Notes**](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#final-notes)
* Overall Workflow
* Collaborating on Development
* Submodule Problems
* Problems with Pull Requests


[**Appendix A:** Table of useful git commands](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#appendix-a-table-of-useful-git-commands)   
[**Appendix B:** Best Practices](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#appendix-b-best-practices)   
[**Appendix C:** Terms](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/_#appendix-c-terms)   

***

# Introduction
This document provides a simplified overview of git and how to use it within CICE-Consortium development.  In most cases, it does not fully represent the details and complexity associated with git.  It should provide a starting point for working in the CICE-Consortium, and it will hopefully encourage users to look for more detailed documentation on the web.  This document is not a substitute for a proper and detailed git user guide.  

If any information is confusing or missing, please provide feedback thru the bulletin board which can be found on the [resource page](https://github.com/CICE-Consortium/About-Us/wiki/Resource-Index).

## General Recommendations
* _Create your own forks for each repository._

* Keep your fork master consistent with the Consortium master:
_pull from the Consortium master and push to your fork master_  

* Work on branches in your sandbox, not on master.
Always branch from master unless you specifically want changes from another branch in the new branch.
Use different sandboxes for different branches.
_Never push changes to your fork master, only to branches._

* _Before a Pull Request, [update your branch](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance#update-a-branch-from-consortium-master) using the Consortium master as your upstream source._

* _Before a Pull Request run the appropriate tests (see [Resource Guide](https://github.com/CICE-Consortium/About-Us/wiki/Resource-Index#model-testing) for details) and include test information in the PR template._

* _Separate updates into multiple Pull Requests (one "fix" at a time)._ Fill in the Pull Request template with details specific to each particular "fix". This is especially important if some changes are bit-for-bit and others are not. 

* Be very careful with every pull and push command to make sure it's from/to the right repo/fork/branch and contains what is intended.  
_Use ‘git status’ and ‘git remote -v’ frequently._

* When working with CICE, treat Icepack as a separate repository.  If you need to modify both Icepack and CICE together, clone your own version of Icepack to use within CICE, create a new branch in each, and commit and push Icepack and CICE changes separately.  Do not worry about the submodule status initially.

See also our [Software Development Practices](https://github.com/CICE-Consortium/About-Us/wiki/Software-Development-Practices).

## Git Overview
CICE consists of a top level driver and dynamical core plus the Icepack code which is included as a git submodule.  Because Icepack is a submodule of CICE, Icepack and CICE development are handled somewhat independently with respect to the github repositories even though development and testing may be done together and in the same sandbox.  

Only a limited number of users are able to push to the CICE-Consortium repositories.  Users will be working on personal forks and executing pull requests to merge their changes into the CICE-Consortium repositories.  If you plan to work within the CICE-Consortium project, create a github account (https://github.com) if you don’t have one already.

A good tutorial on the overall git workflow is at [atlassian's comparing-workflows page](https://www.atlassian.com/git/tutorials/comparing-workflows).  We will be following most of the ideas discussed in those workflows.  Details about using git can be found at the git-scm site or use google search.

There are a few basics to understand about git.  It is distributed.  That means there are actually multiple repositories.  For instance, normally there will be the github CICE-Consortium repository, a user’s github forked repository, and a local repository on your local machine associated with your sandbox.  The sandbox just contains a particular version from your repository like the head of a specific branch.  The sandbox is where you work.  To download a copy of the repository to a local file system, you clone it in git, that creates the local repository and sets up the sandbox.  That sandbox will be set to the head of the master branch initially and will contain all branches and tags from the remote repository at the time of the clone.  You can update your local repository from any other repository by using fetch and merge (aka pull).  When you commit, you are migrating changes from your sandbox to your local repository.  Use push to migrate changes in the local repository back to your fork.  Once your fork is ready, those changes will be migrated to the CICE-Consortium repository by executing a pull request.   To update your local sandbox, you execute a pull from a github repository.  More generally, you can pull or push from/to any github repository.

<!---
![repodiagram](https://github.com/CICE-Consortium/About-Us/wiki/images/CICE_repo_diagrams1.png)
-->

<img src="https://github.com/CICE-Consortium/About-Us/wiki/images/CICE_repo_diagrams1.png" width="500" title="repodiagram">

_**Figure: Relationship between CICE consortium repositories and git commands**_

# Getting Started with Git

## Setup a Github Account

You can clone (checkout) the CICE-Consortium code without a Github account, but if you want to have your own repository and contribute, you'll need a Github account.  To setup a Github account, go to [github.com](https://github.com) and click on the SignUp button in the upper right hand side.

Thereafter, you will SignIn when you go to github.com.

## Local Git Initialization
Before using git on any platform, it’s useful to set a few things.  Execute the following commands,

      git config --global user.name "Your Github Username"
      git config --global user.email you@yourdomain.com
      git config --global push.default simple

You only need to set these once for each independent platform, they will be stored in the file ~/.gitconfig

## Setting Up Github Forks

Users should create personal github forks of CICE and Icepack to carry out any development of the CICE or Icepack source code.  To create a fork (you do this once), 
* Go to the repository page (ie. https://github.com/CICE-Consortium/CICE or https://github.com/CICE-Consortium/Icepack)
* In the upper right hand corner, click on “fork”
* Click on your github avatar/username
* A fork will be created on your github page (ie. https:// github.com/username/CICE)

Each repository (CICE and Icepack) have to be forked separately and users are encouraged to fork both repositories.

We encourage development on branches in forks and for the fork master to generally remain up to date with the Consortium version.  This makes it easier to branch in the fork from a Consortium version of master.

## Updating Your Github Fork master

We’re getting a little ahead with respect to documentation but to keep your fork master up to date with the consortium master, pull from the CICE-Consortium to your local sandbox, commit locally, and then push those changes to your fork.  Typically, this looks like for Icepack

      git clone https://github.com/username/Icepack
      cd Icepack
      git remote add upstream https://github.com/CICE-Consortium/Icepack
      git pull upstream master
      git push origin master

and for CICE

      git clone https://github.com/username/CICE 
      cd CICE
      git remote add upstream https://github.com/CICE-Consortium/CICE
      git pull upstream master
      git push origin master

This entire process clones your fork master which creates a local repo and sandbox, pulls changes from the CICE-Consortium (ie. upstream) master into your local sandbox (which commits those changes to your local repository), and pushes those changes to your fork (origin).  We encourage all users to NOT commit local changes to master (always work on a branch), and to keep the fork master up to date with the consortium master.

## Git Collaborators

In general, your forks are public, anyone can read, but nobody can write.  You can add collaborators to your fork by logging into github and going to the repository, e.g. https:// github.com/username/cice, clicking on Settings, then Collaborators.  Then add the collaborator at the bottom of the page.  When you do, that person will be invited to collaborate on your fork and you can give them write permission.

# Clone, Commit, Branch

## Clone 
**(checkout or creating a Sandbox)**

To create the initial sandbox, use git clone.

      git clone https://github.com/username/CICE --recursive

--recursive populates all submodules, which is useful for CICE since Icepack is a submodule.  If you forget to use --recursive then

      git clone https://github.com/username/CICE
      cd CICE
      git submodule update --init

When you clone, your sandbox will be set to the head of the master branch.  You can also specify a local directory name with git clone 

      git clone https://github.com/username/CICE --recursive CICE.mysandbox

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

Branches and forks are often treated the same, but they are fundamentally different. A fork is a copy of an entire repository; that repository contains branches. A branch is more like a specific version within a repository.  

To see which branches exist, in a sandbox,

      git branch --list
      git branch --list --all

--all shows all remote branches.  To switch to an existing branch, use `git checkout`, then `git submodule update`.

      git checkout branchname
      git submodule update --init  # needed to synchronize your Icepack checkout.
      # or, do both in one command :
      git checkout --recurse-submodules branchname

You can also checkout a branch directly with clone using the -b option from any github location,

      git clone -b branchname https://github.com/username/CICE --recursive

To create a new branch, initialize your sandbox to the version you want to branch from and type,

      git branch mybranch

You will usually branch from the head of the consortium master, and this is good time to update your fork's master as part of the process,

      git clone https://github.com/username/CICE cice.mybranch
      cd cice.mybranch
      git remote add upstream https://github.com/cice-consortium/CICE
      git pull upstream master
      git push origin master
      git branch mybranch
      git checkout mybranch
      git submodule update --init

The first 5 lines above just update master in your fork with the consortium version.  Then the branch is created from the head of master, it is checked out, and then the submodule is checked out.  

We recommend that you give your branches meaningful names, because you likely will create and use many of them, and this helps identify pull requests.  E.g. for a bug fix, you might use something like “bugfix_thermo_conductivity.”  We recommend you work only on branches in your fork and that master is consistent with the CICE-Consortium repository.  **NOTE: When you execute “git checkout”, you will switch branches and may lose local modifications that have not been committed so BE CAREFUL with checkout.** You can use “git stash” to save local changes and then recover them later.

Branches in git are generally not something that should last forever, and they can be used liberally.  As a general rule, pull requests will be done to the Consortium from branches in your fork, and we recommend that each branch be used for a single pull request.  In other words, once a pull request is issued, stop development on that branch and create a new branch.  To branch from a working branch

      git checkout currentbranch
      git branch newbranch
      git checkout newbranch
      git submodule update --init

or even better

      git clone https://github.com/username/CICE cice.mybranch
      cd cice.mybranch
      git remote add upstream https://github.com/cice-consortium/CICE
      git pull upstream master
      git push origin master
      git branch newbranch
      git checkout newbranch
      git pull origin oldbranch
      git submodule update --init

This branches off the current Consortium master but then pulls in any changes to the newbranch from the oldbranch.

To delete a branch in your local repository

      git checkout master
      git branch -d branchname

To delete a branch in your remote repository

      git push origin --delete branchname

If your branch has a submodule (all CICE branches should since Icepack is a submodule!), when you switch to the branch, you may want to update your submodule via a sync and update call,

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

When you `git add` or `git rm` files, `git status` will no longer show them as being different, but they are NOT yet committed to your local repository.  You must do `git commit` to commit the actual code changes.

# Pushing and Pulling

Pushing and Pulling are operations associated with migrating changes between repositories.  You push something if you are acting on the “sending” side and you pull something if you are on the “receiving” side.  To push or pull, you should specify both the repository and what is being migrated explicitly, and you will need write access to that repository.  The git remote command is extremely useful in push and pull operations.

## Remotes

      git remote -v
         origin    https://github.com/username/CICE (fetch)
         origin    https://github.com/username/CICE (push)

shows the repositories that are currently associated with your local repository.  By default, the repository that was cloned will be nicknamed “origin”.  Others can be added easily, e.g.,

      git remote add upstream https://github.com/CICE-Consortium/CICE
      git remote add buddy https://github.com/anotherusername/CICE
      git remote -v
         buddy    https://github.com/anotherusername/CICE (fetch)
         buddy    https://github.com/anotherusername/CICE (push)
         origin    https://github.com/username/CICE (fetch)
         origin    https://github.com/username/CICE (push)
         upstream    https://github.com/CICE-Consortium/CICE (fetch)
         upstream    https://github.com/CICE-Consortium/CICE (push)

Now you can pull or push from/to any of these repositories by referencing their nickname.

## Push

Push migrates changes from your local repository to the github repository.  Push looks like

      git push origin mybranch

This pushes mybranch from your local repository to the origin repository.  You push to the repository of interest (ie. origin) and on the branch of interest (ie. mybranch).  You can also push tags,

      git tag mybranch_tag01
      git push origin mybranch_tag01

## Pull, Rebase

Pull migrates changes from a remote repository to your local repository.  Pull looks like

      git pull origin mybranch

This pulls mybranch from the origin repository to your local repository.  It is important to keep your local branch synced up with your remote repository when multiple people are developing in the same repository+branch.  

When you pull, it's possible conflicts will arise.  If they do, git will let you know and you'll have to manually reconcile those conflicts.

When you pull, you are just integrating local and remote commits on a commit-by-commit basis by time.  Another way to operate is to rebase.  When you rebase, the remote commits are checked out and then your local commits are "replayed" on top.  This will change your local commit history, but can be advantageous in terms of keeping track of commit history and doing pull requests.  To rebase,

      git pull --rebase origin branchname

A pull is the same thing as a fetch and a merge.  There are some cases where it may be better to do a fetch, review the changes (git diff), and then do a merge.  So

      git pull origin branchname

Is the same as

      git fetch origin
      git merge origin/branchname

## Some Examples

### Update fork master from Consortium master

As noted earlier in this document, if you want to update your master fork to recent changes in the CICE-Consortium master, you would pull from the consortium and push to your fork as follows

      git checkout master
      git remote add upstream https://github.com/CICE-Consortium/CICE
      git pull upstream master      # pulls upstream repo master to local repo and sandbox
      git push origin master        # pushes your local repo master to your fork

### Update a branch from Consortium master

A similar process can be used to update a branch.  However, on a branch, we recommend using rebase rather than pull.  Pull merges upstream and local changes based on time of commit.  Rebase updates the local repository by first "rebasing" the repository from the upstream source and then "replaying" your local commits on top of the rebase.  That means your local changes are always built on top of the base.  This would look like

      git checkout branchname
      git remote add upstream https://github.com/CICE-Consortium/CICE
      git pull --rebase upstream master
      git push origin branchname

The push works fine if it is just a fast-forward (consistent history) push.  If you have pushed the branch to your remote repository before the rebase, it probably won't be a fast-forward as the history of your local repository and the remote repository have diverged.  To overcome this, you'll have to do one of two things.  Either force the push and overwrite the history on your branch in your repo.  This is perfectly fine if nobody else is working in your branch.  That would look like

      git push --force-with-lease origin branchname

The force-with-lease (versus just force) checks whether you might overwrite non-local commits on your branch before forcing.  This prevents remote commits by others from being lost.  The other option is to switch to a new branch and pull changes from the old branch,

      git checkout master
      git remote add upstream https://github.com/CICE-Consortium/CICE
      git pull upstream master 
      git push origin master 
      git branch newbranch
      git checkout newbranch
      git pull origin oldbranch

Now you have a new branch based on the current Consortium master with changes from the old branch.

Pull and rebase can result in conflicts.  If there are conflicts, they will be reported and you will have to fix them to continue.  With pull, you will have to resolve the conflicts and commit manually.  With rebase, you will have to resolve the conflicts and use git rebase --continue.  See the git documentation for more details about handling conflicts.  In summary, to rebase a branch with conflicts, do the following

      git clone https://github.com/username/CICE --recursive
      git checkout branchname
      git remote add upstream https://github.com/CICE-Consortium/CICE
      git pull --rebase upstream master (or git fetch upstream master; git rebase upstream/master)
      > hand edit conflicts
      git rebase --continue
      git push --force-with-least origin branchname

Your branch will now be rebased to the current master and your pull request should update and reflect that.

### Rejected pushes

If you get a "rejected" error message when you try to push, it's probably because someone else pushed a change onto your remote repository and your local repository is currently behind.  The fix is to update your local repository by doing

      git pull origin branchname

This could result in a conflict that would have to be resolved.

### Push to a different repository

As noted above, you can pull from a repository that is different from your origin repository.  You can also push to a different remote repository.  If you wanted to copy someone else's branch onto your fork, you could

     git clone https://github.com/anotheruser/CICE CICE.branchname
     cd CICE.branchname
     git checkout branchname
     git add myrepo https://github.com/myusername/CICE
     git push myrepo branchname

This is useful in cases where you want to contribute to a remote repository but you don't have write access.  You can push local commits to the branch to your remote repository (your fork) and then issue PRs to propose merges to the other user's repository.


# Pull Request

## PR Overview

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

There are times where a PR is conflicting with the destination code, where the PR shows changes related to pulls from master, where the PR isn't running correctly, or where the PR just is not reviewable or readable for various reasons.  One option is to pull (or pull --rebase) the Consortium master to your branch.  Sometimes this creates problems for the PR.  Another option is to create a new branch and reissue the PR.  Lets assume the current branch is called feature.  These steps (or similar) should allow you to continue fairly quickly

     (delete pull request for feature branch)
     git clone https://github.com/user/cice cice.feature2
     cd cice.feature2
     git remote add upstream https://github.com/cice-consortium/cice
     git pull upstream master
     git push origin master
     git branch feature2
     git checkout feature2
     git pull origin feature
     git submodule update --init
       (review and test)
     git add ...
     git commit -m "pull feature branch to feature2 branch"
     git push origin feature2
     (create pull request for feature2 branch)

# Submodules

## Submodule Overview

Icepack is a submodule of CICE.  Submodules are pointers to specific versions in an external repository.  Working with Icepack in CICE is like working with a repository in a repository.  When Icepack is cloned by CICE as a submodule, a specific version of Icepack will be downloaded.  Without going into too much detail, Icepack will in a detached HEAD state which means it is a fixed version and cannot be modified easily.  

      git clone https://github.com/username/cice --recursive
      cd cice/icepack
      git remote -v
         origin    https://github.com/CICE-Consortium/Icepack (fetch)
         origin    https://github.com/CICE-Consortium/Icepack (push)
      git status
         HEAD detached at 192fbaa
         nothing to commit, working directory clean

In this case, the CICE has downloaded Icepack hash is 192fbaa from the CICE-Consortium repository into the CICE directory structure.

## Update Icepack in CICE

If all you want to do is change the Icepack version in CICE in the Consortium repository, then you would create a branch, switch the Icepack version, git add Icepack in CICE, commit, and issue a pull request,

      git clone https://github.com/username/CICE cice.mybranch 
      cd cice.mybranch
      (update to Consortium CICE master if needed)
      git branch mybranch
      git checkout mybranch
      git submodule update --init
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

This is the standard procedure for updating the Icepack submodule in CICE.

## Resync Icepack in CICE

As indicated in the [pull and rebase section](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/#pull-rebase), you will want to update the Icepack submodule whenever you change branches or pull from another repository or branch.  You can do that with

      git submodule sync
      git submodule update --init

**NOTE: if you have cloned your own version of Icepack in CICE, do NOT do this as you may lose local changes.**

## Development of Icepack under CICE

When you checkout CICE, a specific version of Icepack will also be cloned.  This version is not ready for modifications, and it can be convenient to develop Icepack changes from a CICE sandbox to facilitate testing within CICE.  You can clone a working version of Icepack to sit within CICE easily as follows,

      git clone https://github.com/username/CICE --recursive CICE.icepack.feature   # checkout CICE
      cd CICE.icepack.feature
      mv Icepack Icepack.00                            # move the default Icepack
      git clone https://github.com/username/Icepack    # clone Icepack separately
      cd Icepack
      git branch feature
      git checkout feature

You now have a copy of Icepack from your personal fork on a new branch in your CICE sandbox.  You can develop, test, commit, and push Icepack changes.  You can also test CICE in this sandbox.  Eventually, you can create an Icepack Pull Request.  In this mode of development, you will probably not be committing any changes to the CICE repository nor should you worry about anything related to the submodule in CICE.  You are just developing Icepack within a CICE sandbox.

## Develop CICE and Icepack Concurrently

There are a number of different ways to handle development of Icepack and CICE concurrently.  What we strongly recommend is that you checkout CICE and Icepack from your fork and develop each within a single sandbox but as independent repositories.  Eventually, you'll do a PR for Icepack.  Once that is accepted, you can [update the submodule in CICE](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/#Update-Icepack-in-CICE) and create a CICE PR.  The basic steps are

1.  clone CICE from user repository (fork)
1.  update CICE repository master to Consortium version if needed
1.  create and checkout a CICE branch
1.  remove/move Icepack
1.  clone Icepack from user repository (fork)
1.  update Icepack repository master to Consortium version if needed
1.  create and checkout an Icepack branch
1.  develop/commit/push Icepack changes to the Icepack remote repository on the Icepack branch.  Develop/commit/push CICE changes to CICE remote repository on the CICE branch.  **Do not update the Icepack submodule in CICE**
1.  execute a PR for the Icepack branch to merge changes to the Consortium repository
1.  update the CICE branch submodule to point to the appropriate Consortium Icepack version and commit/push that change to the CICE branch
1.  execute a PR for the CICE branch to merge changes to the Consortium repository including the update to the Icepack submodule version

By using this approach, the Icepack submodule in CICE is updated only as final step using an existing version of Icepack from the Consortium repository.  The above steps would look like

      git clone https://github.com/username/CICE cice.mybranch --recursive
      cd cice.mybranch
      (update to Consortium CICE master if needed)
      git branch mybranch
      git checkout mybranch
      mv icepack icepack.orig                              # put aside the original version of icepack
      git clone https://github.com/username/Icepack        # check out a new version of icepack from your fork and drop it into your icepack directory in your sandbox
      cd Icepack
      (update to Consortium Icepack master if needed)
      git branch icebranch
      git checkout icebranch
      (modify icepack and cice, test icepack and cice, add/commit/push icepack and cice, as separate repositories)
      git push origin icebranch                            # push all changes to Icepack repository
      (create a PR for icebranch and wait for the Icepack PR to be done)

      cd cice.mybranch
      mv icepack icepack.new                               # put aside your working copy of icepack
      git clone https://github.com/cice-consortium/icepack icepack      # check out the consortium icepack master
      diff -r icepack icepack.new                          # just make sure it looks OK
      (test CICE)
      git add icepack
      git commit -m "update icepack version"
      git push origin mybranch
      (create a PR for CICE that will include CICE mods and a new version of Icepack)

Basically, you are treating CICE and Icepack as separate repositories until the final step where you update the Icepack submodule version in CICE.

## Switch the Icepack Submodule Repository

Two things define a specific version of a submodule, the repository of the submodule and the version (hash).  These two parameters are defined separately, and it's quite possible to end up with a repository and hash that are inconsistent.  In that case, the Icepack submodule won't be valid.  

The Icepack submodule in CICE is generally going to point to the CICE-Consortium Repository.  The [update Icepack in CICE section](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/#Update-Icepack-in-CICE) documents how to update the Icepack submodule version (hash) in CICE.  This section will document how to change the submodule repository.  If you follow the recommended workflow, **you should NEVER do this**.  But for completeness, we include it in the documentation.  To update the submodule repository, you will execute some git config commands,

      git clone https://github.com/username/CICE cice.mybranch --recursive
      cd cice.mybranch
      (update to Consortium CICE master if needed)
      git branch mybranch
      git checkout mybranch   # work on CICE branch
      git config --file=.gitmodules -l
      git config --file=.gitmodules submodule.icepack.url https://github.com/username/Icepack.git  # change the repository
      git config --file=.gitmodules submodule.icepack.branch master
      git config --file=.gitmodules -l
      git submodule sync                          # this syncs to the new submodule.icepack.url repo
      git submodule update --init                 # this checks out the new repo
      cd icepack
      git remote -v                               # verify origin
      git checkout something                      # change the version of Icepack
      cd ../
      git add icepack
      git commit -m "switch icepack to different repository and hash"
      git push origin mybranch

Again, this should be avoided in most cases.  We recommend [Developing CICE and Icepack concurrently](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/#Develop-CICE-and-Icepack-concurrently) and treating the two repositories independently until the Icepack submodule in CICE can be easily updated from a version on the Consortium master.

## Remove and Replace the Icepack Submodule

This is not something you should normally do, but it's another way to change the Icepack submodule repository,

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

# Final Notes

## Overall Workflow

To summarize, a typical workflow for development on a branch would be

      git clone https://github.com/username/CICE cice.mybranch --recursive
      cd cice.mybranch
      git remote add upstream https://github.com/cice-consortium/CICE
      git pull upstream master
      git push origin master
      git submodule update
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
      git pull --rebase upstream master
         (test)
      git commit -m "rebase to master"
      git push origin mybranch
      (create the Pull Request)

## Collaborating on Development

Collaboration on model development features is encouraged.  When collaborating, there are some things to consider

* Communicate regularly regarding working branches, priorities, and pushes.
* Define a prime repository for the work to exist and either provide write access to others or PR changes from other working repositories to the prime repository.
* Use `git pull prime_repo branchname` frequently to ensure your local repository is up to date with the prime repository.
* If a push is rejected, your local repository is behind the prime repository.  Use `git pull prime_repo branchname` to fix this.
* Conflicts can arise, you'll need to resolve them occasionally.
* If working collaboratively on both CICE and Icepack at the same time, be particularly careful to communicate changes.  Try to avoid committing changes to the Icepack submodule in CICE unless it's well thought out.

## Submodule Problems

It's easy to accidently update the Icepack submodule in CICE when you don't mean to.  If Icepack has been modified, updated, or switched in a CICE sandbox, that will show up as an Icepack difference in `git status`.  If you do `git commit -a` you will automatically change the Icepack submodule hash in CICE.  To undo that, the recommended procedure would be to formally [update Icepack in CICE](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance/#Update-Icepack-in-CICE) to the correct version and then continue working.  That might involve moving your working Icepack directory, checking out a version of Icepack from the Consortium, switching to the correct version (hash), and then committing Icepack to CICE.  You can then move your working version of Icepack back into your sandbox.

We suggest avoiding `git commit -a` if there are Icepack changes.  Use `git add` and `git commit` to explicitly add the set of changes that are desired.  You can use `git add` on a directory to add everything under that directory to speed up the process.

If you really get stuck, create a new sandbox and start again.  Do not delete the old sandbox in case you need to recover anything.  You can checkout things again from scratch and try to carefully step forward using the appropriate process.   Also, feel free to contact folks in the Consortium thru the bulletin board for help.  The bulletin board is linked on the [resource page](https://github.com/CICE-Consortium/About-Us/wiki/Resource-Index).

## Problems with Pull Requests

Sometimes a pull request will have conflicts with the current master.  Those conflicts will need to be resolved before the pull request can be executed.  In those cases, the development branch should be updated to any changes from the Consortium Master.  That process is documented in the section related to [updating a branch from the Consortium master](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance#update-a-branch-from-consortium-master)

Sometimes a pull request will reflect more than just the changes you've committed.  That can occur when the history of the branch and the history of the master become intertwined.  Git creates differences by looking at the git history, not at the code differences.  There are a few ways to correct this.  The method we recommend is to create a new branch off the current master, pull the changes from the prior branch to the new branch, then issue a new PR.  These steps are documented in the section on how to [refresh your PR](https://github.com/CICE-Consortium/About-Us/wiki/Git-Workflow-Guidance#refreshing-your-pr)


***

# Appendix A: Table of Useful git Commands

These commands are generally invoked by `git [command]` with some options.

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
 | rebase | like pull but updates the base version then replays local changes, same as pull --rebase |
 | remote [-v] [add] | 	Lists/Sets remote repositories in a sandbox |
 | rm | Removes a file from the repo |
 | status    | Provides summary of status of sandbox |
 | submodule | 	Many options, useful for working with submodules |
 | tag -a | Create a tag or list tags |
 | update | Pull updates into the local sandbox |

### Further Information

There are many git commands to diagnose the status of your sandbox.

#### Status
Status provides a summary of the status of your sandbox.  

      git status

will indicate which branch your sandbox is on and the changes that have been made.  This should be used often during development and before commits and pushes.

#### Diff
Diff shows code changes.

      git diff

#### Log
Log summarizes the commits and pushes in your sandbox up to the current state.  The first entry will provide the id of the current model version.

      git log

If you want a useful graphical summary of the log, try

      git log --graph --oneline --decorate

#### Remote
Remote summarizes the remote repositories setup locally.

      git remote -v

`git remote add` is used to add name new remote repositories for use locally.

***

# Appendix B: Best Practices
* Create a fresh clone and branch for each batch of changes that will be submitted in separate PRs, if a previous PR might not be executed before work begins on the next one.
* Keep your fork master up to date with the Consortium, don't commit local changes to your fork master, and rebase your branches from the main Consortium repositories periodically. 
* Always develop on a branch, then create a PR to merge to the consortium master.
* Use “git status” often.
* Use “git remote -v” often.
* Always commit with a reasonably detailed and clear commit message.

***

# Appendix C: Terms
_Branch_ - A pointer to a parallel development in a repository    
_Checkout_ - When you switch to a branch in your local repository    
_Commit_ - When you copy changes into your local repository    
_Clone_ - When you copy a github repository into a local sandbox    
_Fetch_ - When you update your local repository from an external repository    
_Fork_ - When you copy a repository within github from one github project to another    
_Hash_ - Particular version in git defined by a string of random characters generated by git    
_Master_ - The main or trunk branch in a github repository    
_Merge_ - Merging changes from your local repository to your sandbox    
_Pull_ - When you copy changes out of an external repository to your local repository and merge those changes into your local sandbox.  This is a combination of fetch and merge    
_Pull Request_ - A github operation to request an update to an upstream repository (aka PR)    
_Push_ - When you copy changes into a github repository    
_Sandbox_ - Your local checkout with or without local modifications    
_Submodule_ - An external repository included in another repository    
_Tag_ - The ability to explicitly name a specific version of the module in a repository    

