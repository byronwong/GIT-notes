
4.Committed Environment
=======================

[0. Contents](00-Contents.md)
[1. Setting Up Git](01-SettingUpGit.md)
[2. Working Environment](02-WorkingEnvironment.md)
[3. Staging Environment](03-StagingEnvironment.md)
[4. Committed Environment](04-CommittedEnvironment.md)
<!-- TOC -->

- [Writing commit messages](#writing-commit-messages)
- [Reading Commit Log](#reading-commit-log)
- [Editing a Commit](#editing-a-commit)
- [Undoing Commits](#undoing-commits)
    - [Method 1a - adding a file to the commit](#method-1a---adding-a-file-to-the-commit)
    - [Method 1b - changing the commit message](#method-1b---changing-the-commit-message)
    - [Method 2 - rollback a file several commits before (Single File)](#method-2---rollback-a-file-several-commits-before-single-file)
    - [Method 3 - Revert the commit (Basically reverse the commit to undo changes)](#method-3---revert-the-commit-basically-reverse-the-commit-to-undo-changes)
    - [Method 4 - Rollback multiple commits by moving the HEAD](#method-4---rollback-multiple-commits-by-moving-the-head)
    - [Method 4a - Soft Reset (just moves the HEAD pointer) (safest)](#method-4a---soft-reset-just-moves-the-head-pointer-safest)
    - [Method 4b - Mixed Reset (default)](#method-4b---mixed-reset-default)
    - [Method 4c - Hard Reset (destructive)](#method-4c---hard-reset-destructive)
- [Navigating The Commit Tree](#navigating-the-commit-tree)
- [Listing Commits](#listing-commits)
- [Seeing a commit](#seeing-a-commit)

<!-- /TOC -->
[5. Remote Environment](05-RemoteEnvironment.md)
[6. Branching](06-Branching.md)
[7. Utility](07-Utility.md)

## Writing commit messages

1. single line description 

  `git commit -m "commit text"`

2. line break - TBC

3. more complete description
  - write in the present tense
  - use * or - for bullets
  - use ticket numbers for bugs
  - can use shorthand "[css,js]" "bugfix" "t3355"


    Example:
    t235445- Fixes bug in admin logout

    When admin logged out of admin area they could not log 
    into members area. This patch fixes the bug by setting 
    the session to nil when any use logs out of any area.

## Reading Commit Log

	git log   // returns commit log

	git log -n 10   // returns the next ten logs

	git log --until=2016-01-02
	git log --since=2016-01-02

	git log --author="joe"

	'cat .git/HEAD'   // get location of head
		
	'cat .git[returned location]'   // gives you the HASH that HEAD is at location is provide from above command


## Editing a Commit 

https://help.github.com/articles/changing-a-commit-message/

 If the commit has not been pushed online:

	git commit --amend

Amending older or multiple commit messages

	Steps as above
	then: git push --force example-branch


## Undoing Commits

You can only amend  last commit as long as nothing depends on it.
This is also where the HEAD is.

### Method 1a - adding a file to the commit

1. Make the change you want
2. Add to staging

	git commit --amend -m "message"


### Method 1b - changing the commit message

You can also use this to edit the commit message.

	git commit --amend -m "message"




### Method 2 - rollback a file several commits before (Single File)
Rollback a file several commits before by creating a new commit that un-done the previous commits.

General Pattern:

	git checkout [commitHASH] -- [fileName]

Example:

	git checkout f7b37afdcefe39 -- Index.html
		// Gets the version of the target file in the target commit
		// Add this to your staging environment
		// You can now commit 
		// It's good practice to make sure the commit message says which commit it reverted (use SHA)


### Method 3 - Revert the commit (Basically reverse the commit to undo changes)
	'git revert [commitHASH]'
		// NOTE: will automatically make the commit
		// You can also edit new commit message.


### Method 4 - Rollback multiple commits by moving the HEAD
Its a good idea to have a copy of git log so we have a reference of all the commits (as windows does not show them)



### Method 4a - Soft Reset (just moves the HEAD pointer) (safest)
	
Moves the HEAD back but does not change anything in staging or working directory
This means you'll have all the future commits in working and staging from the target hash.
Thus you tweak/ edit the future commits and have not lost data.


    A -- B -- C -- D

    If you revert to B from D
    Commits C --> D will be in you working and staging environments so you can re-commit them

    git reset --soft [targetHASH]
    // you can now add/commit new changes
    // remember that copy of log? we still can move the head back to the latest commit as long as no new commit



### Method 4b - Mixed Reset (default)

Moves HEAD to desired commit and then updates the staging with changes to reflect the repository
does not change your working directory

    A -- B -- C -- D

    Revert to B
    Staging only contains B
    Working C --> D (Can still add future changes to to staging and commit)

    git reset --mixed [targetHASH]
    // Moves whatever was in staging before reset into working
    // remember that copy of log? we still can move the head back to the latest commit as long as no new commit


### Method 4c - Hard Reset (destructive)
  - Moves HEAD to target commit
  - Changes working and staging to match the repository
  - NOTE: all commits after target will be lost


    git reset --hard [targetHASH]
      // remember that copy of log? we still can move the head back to the latest commit as long as no new commit




## Navigating The Commit Tree
Git 'tree-ish' - something that points to a commit
We can select a commit in several ways:

    Full or Partial SHA-1 hash `acf87504` or `acf8`
    HEAD
    Branch Reference, tag reference
    Ancestry

    parent commit: // '^' says go up one generation
    -HEAD^,
    acf87504^, 
    master^ 
        
    Also: -HEAD~1   // ~x custom number of generations we want to go up

    Grand parent commit: 
    -HEAD^^,
    acf87504^^,
    master^^,
    HEAD~2

    Great Grand Parent commit: 
    -HEAD^^^,
    acf87504^^^,
    master^^^,
    HEAD~3


## Listing Commits

	git help ls-tree
	git help log

	git ls-tree [tree-ish]
	
	git ls-tree master
		// returns a log of all the files in the commit

	git log --oneline
	git log format=oneline
		// returns a log of commits in one line format

	git log --oneline -x
	git log --oneline -3
		// returns the latest 3 commits

	git log --since="2016-02-20"
	git log --after="2016-02-20"
	git log --until="2016-02-20"
	git log --before="2016-02-20"
	git log --since="2 weeks ago" --until="3 days ago"
	git log --since="2.weeks" --until="3.days"

	git log --author="joe"

  Comparing

	git log 996e015..a7b3f0c    // returns all commits from first hash to last hash specfied

	git log 996e015.. index.html    // return all commits since 996e015 involving index.html

	git log -p    // patch option allows you to see what changed

	git log --graph // shows a graphical log 

	git log --oneline --graph --all --decorate



## Seeing a commit

	git show [SHA hash]
	git show 29c0f23    // shows the diff in commit



Comparing Commits
-----------------
	git diff 996e015..a7b3f0c
		// returns all the differences in the files

	git diff 996e015 index.html
		// return changes from this point in time to now regarding index.html




















