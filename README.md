# git-branching-sanity
Some simple steps to keep you from loosing your mind when branching. This is all based on [A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)

## Main (fixed) branches
These have fixed names
* __master__ - Contains what is running in production, it only gets updated when a deployment is about to occur. No work should ever be done directly in this branch. 
* __qa__ - TBD
* __develop__ - It's branched off from Master and contains what has been tested/reviewed and is ready to be deployed. No work should be done directly in this branch.

## Hotfix branches
Hotfix branches come from the *master* branch. They enable you to fix an urgent issue that has arisen from a recent deployment or a bug in production that cannot wait for the *develop* branch to be ready.

They should be named after the issue/ticket you are fixing and contain *hotfix* in the beginning, for example:

```git
hotfix_8569_webservices_bug
```
__Create a hotfix branch__
```git
git checkout -b hotfix_000_name master
```

## Feature branches
Feature branches contain a feature that is being worked on. It may contain incomplete code and/or broken tests. Each feature branch should be separate. 

They should be named in the following manner:

```git
feature_name
```

If all of the changes being done are grouped in a single ticket/issue they should contain the ticket/issue number in the name
```git
8569_sign_up_wizard_changes
```

If the changes being done are based on multiple tickets/issues they should contain those numbers in the name
```git
8569_8524_9856_sign_up_wizard_changes
```

In some occasions they don't correspond directly or 1:1 to tickets/issues, in that case they should just be named after the feature.
```git
sign_up_wizard_changes
```

__Create a feature branch__
```git
git checkout -b 0000_0000_name_of_feature_branch develop
```

## Push a branch back to origin
*make sure you are located in the branch you want to push, then proceed*
```git
git status
git push origin name_of_branch_i_am_working_on
```

## Update an existing branch
*you must be located in the branch you are going to update, if not then you need to commit any pending changes and switch to the branch you want to update*

```git
git status
git add .
git commit --all -m "Some of my changes"
git push origin name_of_branch_i_am_working_on
```

*now that you have staged/committed your pending changes, you can proceed*
```git
git checkout name_of_branch_i_want_to_update
git pull origin name_of_branch_i_want_to_update
```

## Checkout a branch that is already on your machine
*run git status to see if you have any pending changes on your current branch*
```git
git status
```
*if you have any pending changes you must stage and commit them or discard/stash them*
```git
git add .
git commit --all -m "Some of my changes"
git push origin name_of_branch_i_am_working_on
```
*now that you have no pending changes you can fetch and checkout your branch, if you checkout with un-staged files __it will mess up your branch__*
```git
git checkout name_of_branch_i_want
```

## Checkout a branch that is __not__ on your machine
*run git status to see if you have any pending changes on your current branch*
```git
git status
```
*if you have any pending changes you must stage and commit them or discard/stash them*
```git
git add .
git commit --all -m "Some of my changes"
git push origin name_of_branch_i_am_working_on
```
*now that you have no pending changes you can fetch and checkout your __new__ branch*
```git
git fetch origin
git checkout name_of_branch_i_want_to_get
```

## Delete a __local__ branch
*make sure you are not on that branch and execute*
```git
git status
git branch -D name_of_local_branch_i_want_to_delete
```

## Delete a __remote__ branch
*make sure you are not on that branch and execute*
```git
git status
git push origin --delete name_of_remote_branch_i_want_to_delete
```

## Generate a Pull Request
Depending on the branch type you are using your *source_branch* and *target_branch* will be different

Source | Target
-------|-------
develop | master
qa | tbd
hot_fix | master
feature_branch | develop

*make sure you have no pending changes, and commit them if you do*
```git
git status
git add .
git commit --all -m "Some of my changes"
git push origin source_branch
```

*next, switch to the branch you are targeting and pull*
```git
git checkout target_branch
git pull origin target_branch
```

*go back to your __source_branch__  and merge with your __target_branch__*
```git
git checkout source_branch
git merge target_branch
```

*if you have any conflicts, fix them*

Go get :coffee:

*when there are no conflicts, then stage any changes, commit and push*
```git
git status
git add .
git commit --all -m "Merge of source_branch to feature_branch"
git push origin source_branch
```

*and last, go ahead to the web ui and create a New Pull Request*
