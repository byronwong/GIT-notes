
5.Remote Environment
====================

[1. Setting Up Git](01-SettingUpGit.md)
[2. Working Environment](02-WorkingEnvironment.md)
[3. Staging Environment](03-StagingEnvironment.md)
[4. Committed Environment](04-CommittedEnvironment.md)
[5. Remote Environment](05-RemoteEnvironment.md)
<!-- TOC -->

- [List remotes](#list-remotes)
- [Adding a remote](#adding-a-remote)
- [Remove remote](#remove-remote)
- [Pushing to a remote](#pushing-to-a-remote)
- [Pushing to a different or existing remote (not registered)](#pushing-to-a-different-or-existing-remote-not-registered)
- [Cloning a repository](#cloning-a-repository)
- [Private collaborating](#private-collaborating)
- [Open-source collaborating](#open-source-collaborating)

<!-- /TOC -->
[6. Branching](06-Branching.md)
[7. Utility](07-Utility.md)


## List remotes
```
  git remote
    // returns all the registered remotes that local git knows about
    // -v gives more details (verbose)

  cat .git/config
    // shows the git config file
    // you can see what remotes are registered
```

## Adding a remote

Basic pattern:
```
    git remote add [remote alias] [url]
```
Example:
```
  git remote add origin https://github.com/byronwong/ForecastApp.git
    // registers remote repository in '.git/config'
```

## Remove remote
```
	git remote rm [alias]
		// remove the remote from git config
```

## Pushing to a remote

Basic pattern:
```
  git push [remote alias] [branch]
```
Example:
```
	git push origin master    // if not tracking

	git push    // if tracking
```

## Pushing to a different or existing remote (not registered)

In most cases you want to use the -u option.
```
	git push -u [alias] [branch-name]
```
Example:
```
  git push -u heroku master
```

What this does is setup the heroku/master branch to track remote/master
You can now do cat .git/config to see information on branch master
```
	cat .git/refs/remotes/
	cat .git/refs/remotes/origin/
	cat .git/refs/remotes/origin/master
		// refers to a sha code that the origin/master HEAD is pointing to.
```

## Cloning a repository

Start in a folder of your choice

	git clone [url clone link] [folder name to be created]
	git clone https://github/myproject.com lynda_version

	git clone [url] [target folder] -b
		// allows you to target and pull down a specfic branch


Fetching changes
----------------

Fetching gets changes from the remote repository, however it does not `merge` the changes in.

3 branch analogy:
```
  remote/master ------------ hosted in the cloud

  origin/master ----------- your local version that mirror with remote (when online)

  local/master --------- your local working branch
```
When our teammate makes a changes to the remote branch, we have to do a git fetch to get those changes.
These changes are downloaded to the origin/master on your local computer.
Only by merging origin/master into local/master will those updates be fully synced.
```
	git fetch   // get changes if any from default remote

	git fetch [remote alias]   // get changes from specified remote
```
For merging see [Common merging commands](06-Branching.md#common-merging-commands)
For merging fetched changes [Merging Fetched changes](06-Branching.md#merging-fetched-changes)

## Private collaborating

Add a person to the project through the admin panel
They will then have read and right access


## Open-source collaborating

To make changes first you need to make a fork

Fork, make your own version of the repository, that you have access to
Note: this is separate from the project you cloned

Do you changes.

The go back to the project page and create a pull request.
