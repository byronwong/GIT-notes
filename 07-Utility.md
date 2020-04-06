
7.Utility 
=========
[0. Contents](00-Contents.md)
[1. Setting Up Git](01-SettingUpGit.md)
[2. Working Environment](02-WorkingEnvironment.md)
[3. Staging Environment](03-StagingEnvironment.md)
[4. Committed Environment](04-CommittedEnvironment.md)
[5. Remote Environment](05-RemoteEnvironment.md)
[6. Branching](06-Branching.md)
[7. Utility](07-Utility.md)
<!-- TOC -->

- [0.1. gitignore](#01-gitignore)
- [0.2. Ignoring Tracked files](#02-ignoring-tracked-files)
- [0.3. Remove Untracked files](#03-remove-untracked-files)
- [0.4. Fetch all branches locally](#04-fetch-all-branches-locally)
- [0.5. Cleaning up and Pruning](#05-cleaning-up-and-pruning)
    - [0.5.1. Local clean up](#051-local-clean-up)
    - [0.5.2. Remote](#052-remote)
- [0.6. Setting Up Alias Commands](#06-setting-up-alias-commands)
- [0.7. Useful aliases](#07-useful-aliases)

<!-- /TOC -->

## 0.1. gitignore

1. Create a file called .gitignore
2. Can be specific such as a file name
3. Can use reg ex `*` (wildcard) `?`(query) `[aeiou]`(charset) `[0-9]`(range)
4. Can negate expressions by putting a `!` in front of them
5. Use: `#` to add a comment
```
*.php (ignore all files ending with '.php')
!index.php (don't ignore specifically index.php : tracked)
assets/videos/ (trailing slash means all files in this directory are ignored)
```

Things that would be good to ignore:
	- Compiled code
	- packages and compress files
	- log and database (files that change regularly)
	- operating system generated files, these are files that have nothing to do with the project
	- use uploaded assets (images, pdf, videos)

[Git Help](https://help.github.com/articles/ignoring-files/)
[Git preset rules:](https://gist.github.com/octocat/9257657)
[For something more specific:](https://github.com/github/gitignore)


## 0.2. Ignoring Tracked files

- How to ignore file that are already being tracked by git
- git will not ignore a file if it was tracked before the rule was added
- to do this we must un-track the file

- one way to do this is to remove the files 
```
  rm tempFile.txt
```
- better: 
```
  rm --cached tempFile.txt --> removed file from staging index
    // file still is in the repository
```

## 0.3. Remove Untracked files
```
  git clean

  git clean -n    
    // Test run

  git clean -f
    // Forces it to run
    // Clears untracked files in working
    // files in staging are protected from clean
```

## 0.4. Fetch all branches locally
```
git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done
git fetch --all
git pull --all
```

## 0.5. Cleaning up and Pruning
[Housekeeping](https://railsware.com/blog/2014/08/11/git-housekeeping-tutorial-clean-up-outdated-branches-in-local-and-remote-repositories/)

### 0.5.1. Local clean up
`git branch`
`$ git checkout master`
`$ git branch --merged` - returns merged branches that are safe to delete
`git branch --no-merged` - returns un-merged branches which you will need to decide on use `-D` option to delete

### 0.5.2. Remote
`git branch -r` - 
`git branch -r --merged` - returns remote merged branches

`git remote prune origin --dry-run`

But this (`git branch -r --merged`) command does not provide much information. What if this branch is merged, but still used for feature development. Would be cool to know last commit date and author.This magic snippet provides all required information:
```js
  for branch in `git branch -r --merged | grep -v HEAD`; do echo -e `git show --format="%ci %cr %an" $branch | head -n 1` \\t$branch; done | sort -r
```

Now, you can delete own remote branches, and ask other authors to clean-up theirs:
`git push origin --delete branch-name`

Similar to the one above but for non-merged branches
```js
  for branch in `git branch -r --no-merged | grep -v HEAD`; do echo -e `git show --format="%ci %cr %an" $branch | head -n 1` \\t$branch; done | sort -r
```


## 0.6. Setting Up Alias Commands

Creating shortcuts
Best to go to your user directory

	cat .gitconfig
		// shows global config file

	git config --global alias.[shortcut] "[command]"
	git config --global alias.st "status"
		// creates a shortcut for git status

## 0.7. Useful aliases

	git config --global alias.co checkout
	git config --global alias.ci commit
	git config --global alias.br branch
	git config --global alias.dfs "diff --staged"
	git config --global alias.logg "log --graph --decorate --oneline --abbrev-commit --all"
  
  git config --global alias.fire git add -A && git commit -n -m "FIRE!!!" && git push --force --no-verify
  `alias fire='git add -A && git commit -n -m "FIRE!!!" && git push --force --no-verify'`


