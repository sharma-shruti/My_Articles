# Git-Flow

**Git-flow** is a wrapper around Git. The git flow init command is an extension of the default git init command and doesn't change anything in your repository other than creating branches for you.

Git is an open source distributed version control system that is flexible and easy to use for all kinds of teams, no matter how big or small. To adopt Git in everyday development, a model called Gitflow was introduced by Vincent Driessen to help simplify development and release management. 

The central repository holds two main branches:
* master
* develop

When the source code in the develop branch reaches a stable point and is ready to be released, all of the changes should be merged back into master somehow and then tagged with a release number.

## Supporting branches 
Next to the main branches master and develop, our development model uses a variety of supporting branches to aid parallel development between team members, ease tracking of features, prepare for production releases and to assist in quickly fixing live production problems. Unlike the main branches, these branches always have a limited life time, since they will be removed eventually.
The different types of branches we may use are:

1. **Feature branches** - Feature branches (or sometimes called topic branches) are used to develop new features for the upcoming or a distant future release.

```
* May branch off from:
        develop
* Must merge back into:
        develop
* Branch naming convention:
        anything except master, develop, release-*, or hotfix-*
```
2. **Release branches** - Release branches support preparation of a new production release. They allow for minor bug fixes and preparing meta-data for a release (version number, build dates, etc.). By doing all of this work on a release branch, the develop branch is cleared to receive features for the next big release.

```
* May branch off from:
    develop
* Must merge back into:
    develop and master
* Branch naming convention:
    release-*
```
3. **Hotfix branches** - They arise from the necessity to act immediately upon an undesired state of a live production version. When a critical bug in a production version must be resolved immediately, a hotfix branch may be branched off from the corresponding tag on the master branch that marks the production version.
```
* May branch off from:
    master
* Must merge back into:
    develop and master
* Branch naming convention:
    hotfix-*
```

The one exception to the rule here is that, when a release branch currently exists, the hotfix changes need to be merged into that release branch, instead of develop. 
Back-merging the bugfix into the release branch will eventually result in the bugfix being merged into develop too, when the release branch is finished. 
