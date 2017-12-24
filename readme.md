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

To view the current status of these three areas, one can use `git staus`

## commit
* fundamental of git
* takes snapshot of local files and stores reference to it
* each commit is being identified with its unique SHA-Hash

### when to commit
* each commit should have a single focus on a change/feature

### good commit messages
#### do
* keep the message short (less than 60 characters)
* explain what the commit does
#### don't
* explain why changes are made
* explain how changes are made
* use the word 'and'
	* if 'and' must be used it would have been better to split the changes into two seperate commits

If it has to be explained why a change has been made, the explanation should be written on a seperate line (under the first line containing the message).

Further, a style guide for commit messages can be found [here](https://udacity.github.io/git-styleguide/ "udacity's commit message style guide")

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

# Git ignore
If certain files should be ignored and not be added to the repository (e.g. CMake stuff), one may use the `.gitignore` file. Files can be exluded from the repository by just adding its name to the `.gitignore` file. Alternatively 'Globbing' can be used to exclude certain groups of files.

## Globbing Crash Course
lobbing lets you use special characters to match patterns/characters. In the .gitignore file, you can use the following:

### syntax
* blank lines can be used for spacing
* \# - marks line as a comment
* \* - matches 0 or more characters
* ? - matches 1 character
* [abc] - matches a, b, or c
* \*\* - matches nested directories - a/**/z matches:
	* a/z
	* a/b/z
	* a/b/c/z

### examples
* f*		<-> foo && fasdf && ...
* f??		<-> foo && fas   && ...
* [a-z][a-z]	<-> ab  && jf    && ...
* [aA][bB]	<-> aB  && Ab    && ...

**NOTE:** globbing in the `.gitignore` file is case-insensitive.

# useful stuff
* create repos of project skeletons (e.g. java webapp) and clone them when needed

