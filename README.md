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
git checkout -b 0000_0000_name_of_feature develop
```

## Push a branch back to origin
*make sure you are located in the branch you want to push, then proceed*
```git
git status
git push origin name_of_feature
```

## Checkout a branch that has been pushed to origin by someone else
*run git status to see if you have any pending changes on your current branch*
```git
git status
```
*if you have any pending changes you must stage and commit them or discard/stash them*
```git
git add .
git commit --all -m "Some of my changes"
git push origin 0000_0000_name_of_feature
```
*now that you have no pending changes you can fetch and checkout your new branch*
```git
git fetch origin
git checkout name_of_feature_branch
```

## Generate a Pull Request
Depending on the branch type you are using your *target_branch* will be different

__Source | Target__
develop | master
qa | tbd
hot_fix | master
feature_branch | develop

*make sure you have no pending changes, and commit them if you do*
```git
git status
git add .
git commit --all -m "Some of my changes"
git push origin 0000_0000_name_of_feature
```

*next, switch to the branch you are targeting and pull*
```git
git checkout target_branch
git pull origin target_branch
```

*next, switch to the branch you are targeting and pull*
```git
git checkout target_branch
git pull origin target_branch
```

*go back to your __source__ branch and merge with your __target__ branch*
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
