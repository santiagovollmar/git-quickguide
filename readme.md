# basic terminology

## sections
each git repository consists of three main areas:
	* working directory
	* staging index
	* repository

### dataflow
Each change which is about to be appliad to a git repository goes through the following thre phases:
	1. Files are changed in the working directory.
	2. Changes are added to the staging index. 
	3. Changes in staging index get commited to the repository. Changes which are not in the staging index are ignored.

## commit
* fundamental of git
* takes snapshot of local files and stores reference to it
* each commit is being identified with its unique SHA-Hash

## repository
* directory which contains all files of project and git config files
* made up of commits
* can exist locally and remote

## working directory
* files that are currently loaded in one's computer's file system
* **WARNING:** not the same as current working directory

## checkout
* content in the repository loaded into the working directory

## staging area/index
* holds the data that will go into the next commit
* contents are poised to be added to the repository

## branch
* new line of development diverging from main line
* does not alter the main line
* different branches can be used to try out new things
* can contain "save points"