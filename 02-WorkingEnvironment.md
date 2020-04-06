
2.Working Environment
=====================     
[1. Setting Up Git](01-SettingUpGit.md)
[2. Working Environment](02-WorkingEnvironment.md)
<!-- TOC -->

- [Initialising a repository](#initialising-a-repository)
- [Seeing differences](#seeing-differences)
- [Adding to staging](#adding-to-staging)
- [Renaming Files](#renaming-files)
- [Moving Files](#moving-files)
- [Undoing Changes in working environment](#undoing-changes-in-working-environment)

<!-- /TOC -->
[3. Staging Environment](03-StagingEnvironment.md)
[4. Committed Environment](04-CommittedEnvironment.md)
[5. Remote Environment](05-RemoteEnvironment.md)
[6. Branching](06-Branching.md)
[7. Utility](07-Utility.md)                                                                                      

## Initialising a repository

1) Go to user directory
2) Once in the directory run: 
	
	git init    // Initialise a git repository


## Seeing differences

	git diff, 
	git diff [fileName]
		// shows the difference in files between the the committed and the changes in working directory
		// ignores item in staging


## Adding to staging

	git status
		// reports the difference between our working environment and our staging environment

	git add .
		// add all file changes to ---> staging

	git commit -a
		// adds all files to staging and then commit them.
		// does not work for new files or deleted files.	


Deleting Files
--------------

  Method 1 - Delete the file from the file system

	  git add [fileName]
		  // adds the delete event to the staging area
      
    Commit the change
    DONE!!

 
  Method 2 - Using the shell script

	  git rm [fileName]
      // removes the file from the folder
      // NOTE: this does not go to trash it is deleted
      // stages the delete event 


## Renaming Files

  Method 1:

    Rename a file in the file system
    Git now thinks, original file was deleted and a new file was added.
    Once added to staging git detects the rename, commit as usual 

  Method 2:
  
    git mv [originalFileName] [newFileName],
    git mv secondFile.txt secondaryFile.txt
      // uses the move command to rename the file
      // added to staging index


## Moving Files

	git mv ThirdFile.txt firstDirectory/ThirdFile.txt
		// NOTE: you can move and rename at the same time



## Undoing Changes in working environment
	
	git checkout [file name],
	git checkout -- index.html
		// rollback changes in working  to what is currently on the repository
		// '--' stay on my current branch (as checkout has many uses, this can be confusing)

