
7.Utility 
=========

## Contents
[0. Contents](00-Contents.md)
[1. Setting Up Git](01-SettingUpGit.md)
[2. Working Environment](02-WorkingEnvironment.md)
[3. Staging Environment](03-StagingEnvironment.md)
[4. Committed Environment](04-CommittedEnvironment.md)
[5. Remote Environment](05-RemoteEnvironment.md)
[6. Branching](06-Branching.md)
[7. Utility](07-Utility.md)


## .gitignore

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


## Ignoring Tracked files

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

## Remove Untracked files
```
  git clean

  git clean -n    
    // Test run

  git clean -f
    // Forces it to run
    // Clears untracked files in working
    // files in staging are protected from clean
```

## Setting Up Alias Commands

Creating shortcuts
Best to go to your user directory

	cat .gitconfig
		// shows global config file

	git config --global alias.[shortcut] "[command]"
	git config --global alias.st "status"
		// creates a shortcut for git status

## Useful aliases

	git config --global alias.co checkout
	git config --global alias.ci commit
	git config --global alias.br branch
	git config --global alias.dfs "diff --staged"
	git config --global alias.logg "log --graph --decorate --oneline --abbrev-commit --all"


