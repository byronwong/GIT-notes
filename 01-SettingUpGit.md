
1.Setting Up Git
================

[1. Setting Up Git](01-SettingUpGit.md)
<!-- TOC -->

- [General Shell Commands](#general-shell-commands)
- [Setting up terminal](#setting-up-terminal)
- [Paging](#paging)
- [Configuration Levels](#configuration-levels)
- [Remote config](#remote-config)
- [Setting up on Mac](#setting-up-on-mac)
- [Auto complete on Mac](#auto-complete-on-mac)
- [Auto completing already on windows](#auto-completing-already-on-windows)
- [Mac and linux make sure the git completion script is installed](#mac-and-linux-make-sure-the-git-completion-script-is-installed)
- [On Windows should be setup](#on-windows-should-be-setup)

<!-- /TOC -->
[2. Working Environment](02-WorkingEnvironment.md)
[3. Staging Environment](03-StagingEnvironment.md)
[4. Committed Environment](04-CommittedEnvironment.md)
[5. Remote Environment](05-RemoteEnvironment.md)
[6. Branching](06-Branching.md)
[7. Utility](07-Utility.md)

## General Shell Commands

`which git` - returns the file directory where git is installed

`git --version` - returns the current version of git

`cd ~` - change directory to user root	

`cd ..` - go back up to parent directory	

`ls, dir` - lists the contents of a directory

`ls -la`, `ls -la .git` - shows hidden files

`clear` - clears the console

`cat` - display summary of file

`git help`, `git help [item]`, `git help log` - returns help on the git log command

## Setting up terminal

MAC - terminal upgrade:
[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)


## Paging

`f` - forwards
`b` - backwards
`space` - continue
`q` - quit/end
`ctrl + c` - stop/end
`ctrl + z` - end (use 'ctrl + c' or 'q' first)
`fg` - continue
	

## Configuration Levels

  System(--system) | User(--global) | Project (none)

  git config [--configLevel] [item]
    git config --global

    git config --global user.name "byronwong"
    git config --global user.email "your@email.com"

    git config --list
		// returns config data

	cat .gitconfig
		// allows you to look at the hidden .gitconfig file

	git config --global core.editior "sublime"


## Remote config

	git config --global pull.default simple
	git config --global push.default simple 

	upstream - push the current branch to its upstream branch...

	simple - like upstream, but refuses to push if the upstream branch’s name is different from the local one...
	
	current - push the current branch to a branch of the same name.



## Setting up on Mac

check: 'subl' exists.

	sudo ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl	

then: 		

	git config --global core.editor "subl -n -w"



## Auto complete on Mac

https://github.com/bobthecow/git-flow-completion/wiki/Install-Bash-git-completion

Follow these steps:

	cd ~
		// go to user root

	curl -OL https://github.com/git/git/raw/master/contrib/completion/git-completion.bash
		// enter this code in to download the auto completion script from git hub

	ls -la 
		// look for 'git-completion.bash' file to see if installed	

	mv ~/git-completion.bash ~/.git-completion.bash
		// rename file to add a '.' in front so it becomes a dot file

	~/.bash_profile' or '~/.bashrc 
	nano .bash_profile
		// add to login configuration always add to bash_profile unless you know understand why you don't want to.
		// you can also check this file listing using ls -la

Add this code in to '.bash_profile':

	if [-f ~/.git-completion.bash]; then 
		source ~/.git-completion.bash
	fi

DONE!! Close and reopen terminal


## Auto completing already on windows
  Should already be installed for you.
  Viewing branches with (branch name) - (requires auto-complete first)

## Mac and linux make sure the git completion script is installed

	__git_ps1
		// will return the current branch in prompt as long as you are in the repository
		// our prompt is stored in a variable called prompt sting 1 'PS1'
		// we can see this by doing : 'echo $PS1'

	export PS1="[value]",
	export PS1="\W$(__git_ps1 '(%s) > ')"
		// sets the prompt to what you want	for session

To make this permanent:

	export PS1="\W$(__git_ps1 '(%s) > ')" after our script in batch_profile.


## On Windows should be setup

To check: 

	echo $PS1:
	// returns: 
		\[\033]0;$TITLEPREFIX:${PWD//[^[:ascii:]]/?}\007\]\n\[\033[32m\]\u@\h \[\033[35m\]$MSYSTEM \[\033[33m\]\w\[\033[36m\]`__git_ps1`\[\033[0m\]\n$

If Not do this:

1) Use notepad to create file *.bash_profile* as type *all files*:
2) Enter this (or the one above, bellow is a simple version): 

    export PS1='\W$(__git_ps1 "(%s) > ")'

Save as: *.bash_profile* as type: *all files* in your users directory eg: bbwong.

Then run the command:

	source ~/.bash_profile
