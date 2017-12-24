# what is this?
This is just a collection of some information about git which I may find useful ...

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

# files
* **.git**
	* config	- project specific configurations
	* description	- only used by GitWeb
	* **hooks**	- client- or server-side code to hook into git's lifecycle events
	* **info**	- contains the global excludes file
	* **objects**	- contains all commits
	* **refs**	- contains pointers to commits

# logging
Git automatically logs all commits.

The following commands are used to show these logs
* `git log [hash]`	- basic command
* `--oneline`		- displays compact view
* `--stat`		- displays extended view

Alternatively `git show` can be used to show only one commit.

## display changes
Actual changes in files and of certain commits can be displayed with `git log --patch`. If `-w` is applied, changed whitespace is ignored
Changes are structured like following:

```Diff
diff --git a/{old_file} b/{new_file}					//file being displayed
idex XXXXXXX..XXXXXXX XXXXXX						//hash stuff
--- a/{old_file}
+++ b/{new_file}

@@ -{start_old},{line_count_old} +{start_new},{line_count_new} @@	//describes where edits where made

 {unchanged line}							//shows content which has changed
 {unchanged line}
-{removed line}
-{removed line}
+{added line}
+{added line}
+{added line}
-{removed line}
 {unchanged line}

```

Differences between old and new files can also be displayed with `git diff`

# useful stuff
* create repos of project skeletons (e.g. java cl app) and clone them when needed

