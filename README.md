# The Fezzee Git-Flow
This repo is used to document and test the Fezzee gitflow, and using pull requests for code reviews

Notes-
After initially creating the repo, 

1. In github manually create  the repo, with the name 'gitflowtest'
2. on the local machine, create a directory with the same name as the repo 'gitflowtest'
3. Open terminal and change to the new directory and run:

```
touch README.md
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git remote add origin git@github.com:datumlogic/gitflowtest.git
$ git push -u origin master
```


The next step is to create the devlop branch. In terminal type:

$ git checkout -b develop

Push the branch on github :

$ git push origin develop


# The Paradigm
We consider origin/master to be the main branch where the source code of HEAD always reflects a production-ready state.

We consider origin/develop to be the 'integration branch' where the source code of HEAD always reflects a state with the latest delivered development changes for the next release.
This is where any automatic nightly builds are built from.

When the source code in the develop branch reaches a stable point and is ready to be released, all of the changes should be merged back into master somehow and then tagged with a release number.

Each time when changes are merged back into master, this is a new production release by definition. We should use a Git hook script to automatically build and roll-out our software to our production servers every time there was a commit on master.

Next to the main branches master and develop, our development model uses a variety of supporting branches to aid parallel development between team members, ease tracking of features, prepare for production releases and to assist in quickly fixing live production problems. Unlike the main branches, these branches always have a limited life time, since they will be removed eventually.

The different types of branches we may use are:

* Feature branches- used to develop new features for the upcoming or a distant future release. The essence of a feature branch is that it exists as long as the feature is in development, but will eventually be merged back into develop (to definitely add the new feature to the upcoming release) or discarded (in case of a disappointing experiment). Feature branches typically exist in developer repos only, not in origin.
* Release branches- support preparation of a new production release. They allow for last-minute dotting of i’s and crossing t’s. Furthermore, they allow for minor bug fixes and preparing meta-data for a release (version number, build dates, etc.). By doing all of this work on a release branch, the develop branch is cleared to receive features for the next big release. This phase is called 'Fit and Finish'. Release branches are created from the develop branch. 
* Hotfix branches- very much like release branches in that they are also meant to prepare for a new production release, albeit unplanned. They arise from the necessity to act immediately upon an undesired state of a live production version. When a critical bug in a production version must be resolved immediately, a hotfix branch may be branched off from the corresponding tag on the master branch that marks the production version.

The branch types are categorised by how we use them. They are of course plain old Git branches.

Working with these additional branches, while actually not very difficult, it is somewhat convoluted, so much so that a help script was created to make it less confusing.
https://github.com/nvie/gitflow   Here's a short intro video  https://vimeo.com/16018419

So before we get into all that, lets first demonstrate how we'd use the simple main branches 'develop' and 'master'.

## develop' and 'master'

Here we'll make our changes directly to the 'develop' branch

First we enter:

$ git branch
* develop
  master

to make sure we're working on 'develop'. If not we use this command to change to 'develop':

$ git checkout develop
M	README.md
Switched to branch 'develop'

Once we're made our changes locally, we'll want to commit them:

$ git add -A .
$ git commit -m "updated README.md"
$ git push -u origin develop

Now you could SSH into a Test (Sandbox) environment, and pull the code from 'develop' for testing.




