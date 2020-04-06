
3.Staging Environment
=====================

[1. Setting Up Git](01-SettingUpGit.md)
[2. Working Environment](02-WorkingEnvironment.md)
[3. Staging Environment](03-StagingEnvironment.md)
<!-- TOC -->

- [Seeing differences in Staging](#seeing-differences-in-staging)
- [Committing to Git](#committing-to-git)
- [Committing from working](#committing-from-working)
- [Un-staging Items](#un-staging-items)
- [Stashing](#stashing)

<!-- /TOC -->
[4. Committed Environment](04-CommittedEnvironment.md)
[5. Remote Environment](05-RemoteEnvironment.md)
[6. Branching](06-Branching.md)
[7. Utility](07-Utility.md)

## Seeing differences in Staging

	git diff --staged
		// shows the changes made to items in staging


## Committing to Git

	git commit -m "initial commit"
		// commit to git with message
		// creates a git log of the commit


## Committing from working
	git commit -a   // commits all changes to the repository, even if in working


## Un-staging Items
  Staging ---> Working
	
	git reset HEAD Index.html   // Moves the target file back into working

## Stashing

A place were you can store changes without committing them.
Note: git does not care about the branch, when dealing with stashes this mean you can stash on one branch and commit to another

	git stash save "[message]"    // tells git to save the changes


	git stash list    // returns items in stash


	git stash show [name of stash],
	git stash show stash@{0}
		// shows more details about a specific stash
		// for more details use -p option


	git stash apply [name of stash]
		// moves item from stash but leaves a copy in stash
		// if you don't specify it will take the first one


	git stash pop [name of stash]   // move item from stash and delete it from stash


	git stash drop [name of stash]    // removes item from stash


	git stash clear   // clears all items in stash

