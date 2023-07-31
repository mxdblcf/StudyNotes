# git

#### Git Basics

<details>

<summary>Explain the following: <code>git directory</code>, <code>working directory</code> and <code>staging area</code></summary>

\


This answer taken from [git-scm.com](https://git-scm.com/book/en/v1/Getting-Started-Git-Basics#\_the\_three\_states)

"The Git directory is where Git stores the meta-data and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from another computer.

The working directory is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.

The staging area is a simple file, generally contained in your Git directory, that stores information about what will go into your next commit. It’s sometimes referred to as the index, but it’s becoming standard to refer to it as the staging area."

</details>

<details>

<summary>What is the difference between <code>git pull</code> and <code>git fetch</code>?</summary>

\


Shortly, git pull = git fetch + git merge

When you run git pull, it gets all the changes from the remote or central repository and attaches it to your corresponding branch in your local repository.

git fetch gets all the changes from the remote repository, stores the changes in a separate branch in your local repository

</details>

<details>

<summary>How to check if a file is tracked and if not, then track it?</summary>

\


There are different ways to check whether a file is tracked or not:

* `git ls-files <file>` -> exit code of 0 means it's tracked
* `git blame <file>` ...

</details>

<details>

<summary>Explain what the file <code>gitignore</code> is used for</summary>

\
The purpose of `gitignore` files is to ensure that certain files not tracked by Git remain untracked. To stop tracking a file that is currently tracked, use git rm --cached.

</details>

<details>

<summary>How can you see which changes have done before committing them?</summary>

\
\`git diff\`

</details>

<details>

<summary>What <code>git status</code> does?</summary>

\


`git status` helps you to understand the tracking status of files in your repository. Focusing on working directory and staging area - you can learn which changes were made in the working directory, which changes are in the staging area and in general, whether files are being tracked or not.

</details>

<details>

<summary>You've created new files in your repository. How to make sure Git tracks them?</summary>

\


`git add FILES`

</details>

#### Scenarios

<details>

<summary>You have files in your repository you don't want Git to ever track them. What should you be doing to avoid ever tracking them?</summary>

\


Add them to the file `.gitignore`. This will make sure these files are never added to staging area.

</details>

<details>

<summary>A development team in your organization is using a monorepo and it's became quite big, including hundred thousands of files. They say running many git operations is taking a lot of time to run (like git status for example). Why does that happen and what can you do in order to help them?</summary>

\


Many Git operations are related to filesystem state. `git status` for example will run diffs to compare HEAD commit to index and another diff to compare index to working directory. As part of these diffs, it would need to run quite a lot of `lstat()` system calls. When running on hundred thousands of files, it can take seconds if not minutes.

One thing to do about it, would be to use the built-in `fsmonitor` (filesystem monitor) of Git. With fsmonitor (which integrated with Watchman), Git spawn a daemon that will watch for any changes continuously in the working directory of your repository and will cache them . This way, when you run `git status` instead of scanning the working directory, you are using a cached state of your index.

Next, you can try to enable `feature.manyFile` with `git config feature.manyFiles true`. This does two things:

1. Sets `index.version = 4` which enables path-prefix compression in the index
2. Sets `core.untrackedCache=true` which by default is set to `keep`. The untracked cache is quite important concept. What it does is to record the mtime of all the files and directories in the working directory. This way, when time comes to iterate over all the files and directories, it can skip those whom mtime wasn't updated.

Before enabling it, you might want to run `git update-index --test-untracked-cache` to test it out and make sure mtime operational on your system.

Git also has the built-in `git-maintainence` command which optimizes Git repository so it's faster to run commands like `git add` or `git fatch` and also, the git repository takes less disk space. It's recommended to run this command periodically (e.g. each day).

In addition, track only what is used/modified by developers - some repositories may include generated files that are required for the project to run properly (or support certain accessibility options), but not actually being modified by any way by the developers. In that case, tracking them is futile. In order to avoid populating those file in the working directory, one can use the `sparse checkout` feature of Git.

Finally, with certain build systems, you can know which files are being used/relevant exactly based on the component of the project that the developer is focusing on. This, together with the `sparse checkout` can lead to a situation where only a small subset of the files are being populated in the working directory. Making commands like `git add`, `git status`, etc. really quick

</details>

#### Branches

<details>

<summary>What's is the branch strategy (flow) you know?</summary>

\


* Git flow
* GitHub flow
* Trunk based development
* GitLab flow

[Eplanation](https://www.bmc.com/blogs/devops-branching-strategies/).

</details>

<details>

<summary>True or False? A branch is basically a simple pointer or reference to the head of certain line of work</summary>

\


True

</details>

<details>

<summary>You have two branches - main and devel. How do you make sure devel is in sync with main?</summary>

\
` ``` git checkout main git pull git checkout devel git merge main ``` `

</details>

<details>

<summary>Describe shortly what happens behind the scenes when you run <code>git branch</code></summary>

\


Git runs update-ref to add the SHA-1 of the last commit of the branch you're on into the new branch you would like to create

</details>

<details>

<summary>When you run <code>git branch</code> how does Git know the SHA-1 of the last commit?</summary>

\


Using the HEAD file: `.git/HEAD`

</details>

<details>

<summary>What <code>unstaged</code> means in regards to Git?</summary>

\


A file that is in the working directory but is not in the HEAD nor in the staging area is referred to as "unstaged".

</details>

<details>

<summary>True or False? when you <code>git checkout some_branch</code>, Git updates .git/HEAD to <code>/refs/heads/some_branch</code></summary>

\


True

</details>

#### Merge

<details>

<summary>You have two branches - main and devel. How do you merge devel into main?</summary>

\


```
git checkout main
git merge devel
git push origin main
```

</details>

<details>

<summary>How to resolve git merge conflicts?</summary>

\


First, you open the files which are in conflict and identify what are the conflicts. Next, based on what is accepted in your company or team, you either discuss with your colleagues on the conflicts or resolve them by yourself After resolving the conflicts, you add the files with \`git add \` Finally, you run \`git rebase --continue\`

</details>

<details>

<summary>What merge strategies are you familiar with?</summary>

\


Mentioning two or three should be enough and it's probably good to mention that 'recursive' is the default one.

recursive resolve ours theirs

This page explains it the best: https://git-scm.com/docs/merge-strategies

</details>

<details>

<summary>Explain Git octopus merge</summary>

\


Probably good to mention that it's:

* It's good for cases of merging more than one branch (and also the default of such use cases)
* It's primarily meant for bundling topic branches together

This is a great article about Octopus merge: http://www.freblogg.com/2016/12/git-octopus-merge.html

</details>

<details>

<summary>What is the difference between <code>git reset</code> and <code>git revert</code>?</summary>

\


`git revert` creates a new commit which undoes the changes from last commit.

`git reset` depends on the usage, can modify the index or change the commit which the branch head is currently pointing at.

</details>

#### Rebase

<details>

<summary>You would like to move forth commit to the top. How would you achieve that?</summary>

\


Using the `git rebase` command

</details>

<details>

<summary>In what situations are you using <code>git rebase</code>?</summary>

\
Suppose a team is working on a \`feature\` branch that is coming from the \`main\` branch of the repo. At a point, where the feature development is done, and finally we wish to merge the feature branch into the main branch without keeping the history of the commits made in the feature branch, a \`git rebase\` will be helpful.

</details>

<details>

<summary>How do you revert a specific file to previous commit?</summary>

\


```
git checkout HEAD~1 -- /path/of/the/file
```

</details>

<details>

<summary>How to squash last two commits?</summary>

\


</details>

<details>

<summary>What is the <code>.git</code> directory? What can you find there?</summary>

\
The `.git` folder contains all the information that is necessary for your project in version control and all the information about commits, remote repository address, etc. All of them are present in this folder. It also contains a log that stores your commit history so that you can roll back to history.

This info copied from [https://stackoverflow.com/questions/29217859/what-is-the-git-folder](https://stackoverflow.com/questions/29217859/what-is-the-git-folder)

</details>

<details>

<summary>What are some Git anti-patterns? Things that you shouldn't do</summary>

\


* Not waiting too long between commits
* Not removing the .git directory :)

</details>

<details>

<summary>How do you remove a remote branch?</summary>

\


You delete a remote branch with this syntax:

git push origin :\[branch\_name]

</details>

<details>

<summary>Are you familiar with gitattributes? When would you use it?</summary>

\


gitattributes allow you to define attributes per pathname or path pattern.\


You can use it for example to control endlines in files. In Windows and Unix based systems, you have different characters for new lines (\r\n and \n accordingly). So using gitattributes we can align it for both Windows and Unix with `* text=auto` in .gitattributes for anyone working with git. This is way, if you use the Git project in Windows you'll get \r\n and if you are using Unix or Linux, you'll get \n.

</details>

<details>

<summary>How do you discard local file changes? (before commit)</summary>

\


`git checkout -- <file_name>`

</details>

<details>

<summary>How do you discard local commits?</summary>

\


`git reset HEAD~1` for removing last commit If you would like to also discard the changes you \`git reset --hard\`\`

</details>

<details>

<summary>True or False? To remove a file from git but not from the filesystem, one should use <code>git rm</code></summary>

\


False. If you would like to keep a file on your filesystem, use `git reset <file_name>`

</details>

### References

<details>

<summary>How to list the current git references in a given repository?</summary>

\


`find .git/refs/`

</details>

### Git Diff

<details>

<summary>What git diff does?</summary>

\


git diff can compare between two commits, two files, a tree and the staging area, etc.

</details>

<details>

<summary>Which one is faster? <code>git diff-index HEAD</code> or <code>git diff HEAD</code></summary>

\


`git diff-index` is faster but to be fair, it's because it does less. `git diff index` won't look at the content, only metadata like timestamps.

</details>

<details>

<summary>By which other Git commands does git diff used?</summary>

\


The diff mechanism used by `git status` to perform a comparison and let the user know which files are being tracked

</details>

### Git Internal

<details>

<summary>Describe how `git status` works</summary>

\


Shortly, it runs `git diff` twice:

1. Compare between HEAD to staging area
2. Compare staging area to working directory

</details>

<details>

<summary>If <code>git status</code> has to run diff on all the files in the HEAD commit to those in staging area/index and another one on staging area/index and working directory, how is it fairly fast?</summary>

\


One reason is about the structure of the index, commits, etc.

* Every file in a commit is stored in tree object
* The index is then a flattened structure of tree objects
* All files in the index have pre-computed hashes
* The diff operation then, is comparing the hashes

Another reason is caching

* Index caches information on working directory
* When Git has the information for certain file cached, there is no need to look at the working directory file

</details>
