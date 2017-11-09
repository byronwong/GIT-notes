6.Branching
===========

## Main Contents
[0. Contents](00-Contents.md)
[1. Setting Up Git](01-SettingUpGit.md)
[2. Working Environment](02-WorkingEnvironment.md)
[3. Staging Environment](03-StagingEnvironment.md)
[4. Committed Environment](04-CommittedEnvironment.md)
[5. Remote Environment](05-RemoteEnvironment.md)
[6. Branching](06-Branching.md)
[7. Utility](07-Utility.md)

## Basic commands
```
  git branch    // shows all branches (local)

  git branch -r   // returns remote branches ONLY

  git branch -a   // returns all branches

  cat [filepath]
  cat .git/HEAD   // return HEAD location file path use bellow
  cat .git/refs/heads/master    // returns SHA hash of commit at HEAD
```

## Creating a branch and going to a new branch
```
  git branch [new branch name]    // create [new branch name]
  git checkout [new branch name] // goto [new branch name]

  git checkout -b [new branch name] // create & goto [new branch name]
```

## Creating a remote branch and setup tracking
```
  git push --set-upstream [remote alias] [branch name]
  git push -u [remote alias] [branch name]
```

## Renaming Branch
```
	git branch --move [existing branch name] [new branch name]
	git branch -m [existing branch name] [new branch name]
```

## Deleting Branches
1. Make sure you are on the master branch
2. cannot delete if you are on the branch to delete
```
	git branch --delete  [branch name]
	git branch -d [branch name]
```
3. If there are commits in that branch use -D (force delete) to confirm you want to lose changes


## Deleting a remote branch
```
  git push origin --delete [branch name]]
  git push origin -d [branch name]
  git push origin -D [branch name]
```

## Cleaning up remote branches
```
  git branch -r   // get all branches

  git remote prune origin --dry-run   // lists branches that can be deleted/pruned (remote)

  git remote prune origin   // run prune  
```

## Merging Branches
1. Checkout to the branch you want to receive the changes
2. Then use the following code:
```
  git merge [branch name]

  git merge [branch name] --no-ff  // forces no fast forwarding

  git merge [branch name] --ff    // only do the merge is it is fast forward
```
	
## Merging Conflicts
Merge conflicts when two people make changes to the same document, in most cases conflict occurs with the same part of the document are edited and git does not know which one you want to keep.

Git puts you into a transition environment giving options:

Three options:
	a. abort the merge: 'git merge --abort' - reverts it back to before the merge
	b. resolve conflict manually --> make changes --> add to staging and then commit
	c. use a merge tool 'git mergetool --tool=kdiff3'


Reducing merge conflicts.
- key lines short - don't have a massive paragraph tag
- keep commits small and focused. especially stray edited to white space
- merge often into master, this is so there is less accumulation to changes on master
- if there are a lot of changes to master while you are working on a branch you can merge master changes into your branch. (this process is called tracking)

## Common merging commands
When you do not have a commit
```
  git pull origin master 
```
When you have committed on the branch
```
  git pull origin master --rebase
  git push -f
```

## Merging Fetched changes
```
  git fetch [alias]
  git fetch

  git merge origin/master   // merges origin/master into your local current branch

  git pull    // git fetch + git merge
```

