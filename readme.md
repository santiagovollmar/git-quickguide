# basic terminology

## sections
each git repository consists of three main areas:
 * working directory
 * staging index
 * repository

#### dataflow
Each change which is about to be appliad to a git repository goes through the following thre phases:
 1. Files are changed in the working directory.
 2. Changes are added to the staging index. 
 3. Changes in staging index get commited to the repository. Changes which are not in the staging index are ignored.

To view the current status of these three areas, one can use `git staus`

## commit
* fundamental of git
* takes snapshot of local files and stores reference to it
* each commit is being identified with its unique SHA-Hash
* commits can also be tagged to make them stand out
	* tags can be applied to a commit with `git tag -a {name} [SHA]`.
	* tags can be deleted by applying the `-d` flag

#### when to commit
* each commit should have a single focus on a change/feature

#### good commit messages
##### do
* keep the message short (less than 60 characters)
* explain what the commit does
##### don't
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
Here is a quick overview of git specific files

* `.gitignore`		- files to exclude from staging
* `**.git**`
	* `config`	- project specific configurations
	* `description`	- only used by GitWeb
	* `**hooks**`	- client- or server-side code to hook into git's lifecycle events
	* `**info**`	- contains the global excludes file
	* `**objects**`	- contains all commits
	* `**refs**`	- contains pointers to commits

# logging
Git automatically logs all commits.

The following commands are used to show these logs
* `git log [hash]`			- basic command
* `git log --oneline`			- displays compact view
* `git log --stat`			- displays extended view
* `git log --oneline --graph --all`	- displays an overview of all commits of each branch

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

# git ignore
If certain files should be ignored and not be added to the repository (e.g. CMake stuff), one may use the `.gitignore` file. Files can be exluded from the repository by just adding its name to the `.gitignore` file. Alternatively 'Globbing' can be used to exclude certain groups of files.

## globbing basics
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

# branching
Branches allow for simultaneous development on different features/versions. By default the first branch is called 'master'. Each branch always has a branch pointer, which points to a specific commit. Different branches can diverge from each other on any commit. Each branch has its own commits, its own working directory and its own staging index.

In each git repository there is a HEAD pointer which points to the currently active branch. New commits are always added to the branch which HEAD is currently pointing to.

The `git branch` command is used to interact with git branches.
Usage:
* `git branch`			- show all branches
* `git branch {name} [SHA]`	- create new branch (at commit with specified SHA)
* `git branch -d [name]`	- delete existing branch

To switch between different branches one may use `git checkout {name}`.

# merging
Merging can be used to combine changes of two seperate branches. Branches are always merged into other branches leaving the branch that has been merged into anothter unaffected. For Example: if 'new_feature' is merged into 'master' then 'master' will contain all of its own commits plus the commits from 'new_feature'. However, 'new_feature' is unaffected by this merge. Each merge will create a new commit on the branch being affected. This kind of merge is being refered as a simple 'merge'.
There is, however, another type of merge called the 'fast-forward merge'. It occurs when a branch, which is ahead of another branch, is merged into the other branch.

Whenever a merge occurs git will:
* look at the branches that it's going to merge
* look back along the branch's history to find a single commit that both branches have in their commit history
* combine the lines of code that were changed on the separate branches together
* makes a commit to record the merge

In git branches can be merged with the `git merge` command.

## merge conflicts
Sometimes when performing a merge, git might not be able to combine all changes and places special markers (`>>>` and `<<<`) where files need to manually be fixed.
Merge conflicts will occur, when the same lines have been edited dirrefently in the two seperate branches. Git then won't know which changes to apply to the new commit and will have to ask the user for help.

### conflict indicators
* <<<<<<< HEAD				- everything below this line is in the current branch
* ||||||| merged common ancestors	- everything below this were the original lines
* =======				- end of original lines
* >>>>>>> {branch}			- ending indicator of other branch

To resolve merging conflicts one can just:
1. choose which line(s) to keep or create new
2. remove all lines with indicators
3. add files to staging index and commit

# undoing changes
## changing the last commit
With `git commit --ammend` one can edit the most recent commit. One just has to apply the desired changes to the files, stage them and run `git commit --ammend`. Git will then open the default text editor, prompting the user to enter a new commit message.

## reverting
When Git is being told to revert a specific commit, git will take the changes that have been made in a commit and does the exact opposite of them, which effectively undos all the cnages from that commit. Reverts can be made using `git revert {SHA}`

## resetting
coming soon ...

# remote repositories and collaboration
## what are remote repositories
Remote repositories are repositories managed by a version control system, that aren't on one's personal computer but hosted somewhere else. Remote repositories allow people to collaborate together with relative ease.

## interacting with remote repositories


# useful stuff
* create repos of project skeletons (e.g. java webapp) and clone them when needed
* [interactive tutorial on git branching and merging](https://learngitbranching.js.org/ "interactive git tutorial")
