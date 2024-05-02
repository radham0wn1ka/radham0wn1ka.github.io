---
layout: post
title:  "git github"
date:   2024-05-02 09:29:20 +0700
categories: git github
usemathjax: true
---
- Git is a distributed version control system
- It provides a way to work with one or more local branches and then push them to a remote repository.
- GitHub is a cloud platform that uses Git as its core technology. GitHub simplifies the process of collaborating on projects and provides a website, more command-line tools, and overall flow that developers and users can use to work together. GitHub act s as the remote repository
- Key features provided by GitHub include:


    Issues
    Discussions
    Pull requests
    Notifications
    Labels
    Actions
    Forks
    Projects

- Git is distributed, which means that a project's complete history is stored both on the client and on the server. You can edit files without a network connection, check them in locally, and sync with the server when a connection becomes available
- make a hash and check the file changed or not
- repo,current working dir
- Branch: A branch is a named series of linked commits. The most recent commit on a branch is called the head
-  The default branch, which is created when you initialize a repository, is called main, often named master in Git. The head of the current branch is named HEAD
- Remote: A remote is a named reference to another Git repository. When you create a repo, Git creates a remote named origin that is the default remote for push and pull operations.
- commands sub commands :git pull
- [link from microsoft](https://learn.microsoft.com/en-us/training/modules/intro-to-git/1-what-is-vc)
## git using
-  We tell Git to start tracking changes by initializing a Git repository into that folder.
### sample
```
C:\home\radha\Music\portfolio\jekyll-klise> git status   
On branch main
Your branch is up to date with 'origin/main'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        _posts/git_github/
nothing added to commit but untracked files present (use "git add" to track)            
C:\home\radha\Music\portfolio\jekyll-klise> git add .   
C:\home\radha\Music\portfolio\jekyll-klise> git status
On branch main
Your branch is up to date with 'origin/main'.
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   _posts/git_github/2024-05-02-GitGithub.md           
C:\home\radha\Music\portfolio\jekyll-klise> git commit -m "c2"     
[main 0df674e] c2
 1 file changed, 30 insertions(+)
 create mode 100644 _posts/git_github/2024-05-02-GitGithub.md         
C:\home\radha\Music\portfolio\jekyll-klise> git status        
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
nothing to commit, working tree clean        
C:\home\radha\Music\portfolio\jekyll-klise> 
```
- git add is the command you use to tell Git to start keeping track of changes in certain files.
- The technical term is staging these changes. You'll use git add to stage changes to prepare for a commit. All changes in files that have been added but not yet committed are stored in the staging area
- After you've staged some changes for commit, you can save your work to a snapshot by invoking the git commit command.
- The data that's saved in a commit includes the author's name and e-mail address, the date, comments about what you did (and why), an optional digital signature, and the unique identifier of the preceding commit.
## git-scm
- [link](https://git-scm.com/docs/user-manual)
- [another link](https://git-scm.com/docs/user-manual)
- Git is a fast distributed revision control system.
- single Git repository can track development on multiple branches. It does this by keeping a list of heads which reference the latest commit on each branch
### git tagging
```
C:\home\radha\todo_list> git status
On branch main
Your branch is up to date with 'origin/main'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	todo.csv
nothing added to commit but untracked files present (use "git add" to track)
C:\home\radha\todo_list> git tag
v1
C:\home\radha\todo_list> git add .
C:\home\radha\todo_list> git commit -m "commit after adding todo.csv"
[main 97b152c] commit after adding todo.csv
 1 file changed, 1 insertion(+)
 create mode 100644 todo.csv
C:\home\radha\todo_list> git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
nothing to commit, working tree clean
C:\home\radha\todo_list> git tag
v1
C:\home\radha\todo_list> git branch
* main
C:\home\radha\todo_list> git switch -c b1 v1
Switched to a new branch 'b1'
C:\home\radha\todo_list> git branch
* b1
  main
C:\home\radha\todo_list> 
```
- git switch
- git switch -c is for creating new branch
`git switch [<options>] (-c|-C) <new-branch> [<start-point>]`
- git switch branch_name_to_switch
- git branch new_barnch_name starging_point
- git checkout  -b new_branch_nae starting_point 
- git branch <branch> <start-point>
    create a new branch named <branch>, referencing <start-point>, which may be specified any way you like, including using a branch name or a tag name.
 - git switch 
 - The git switch command normally expects a branch head, but will also accept an arbitrary commit when invoked with --detach; for example, you can check out the commit referenced by a tag
 - swithc to a specifi commit without cretign a new branch for that
 `git switch --detach c`
 ### toread
 - [link1](https://git-scm.com/docs/user-manual)
 - [link2](https://docs.github.com/en/get-started/start-your-journey/git-and-github-learning-resources)
- git reset branch_name
- from a remote branch to create a local branch we use  `git switch -c my_local_new_branch origin/exiiting_branch`
- "origin" is just the name that Git uses by default to refer to the repository that you cloned from
```
Branches, remote-tracking branches, and tags are all references to commits. All references are named with a slash-separated path name starting with refs; the names we’ve been using so far are actually shorthand:
    The branch test is short for refs/heads/test.
    The tag v2.6.18 is short for refs/tags/v2.6.18.
    origin/master is short for refs/remotes/origin/master
```
### git remote add origin
```
The git remote add command takes two arguments:
    A remote name, for example, origin
    A remote URL, for example, https://github.com/OWNER/REPOSITORY.git
$ git remote add origin https://github.com/OWNER/REPOSITORY.git
# Set a new remote
$ git remote -v
# Verify new remote
> origin  https://github.com/OWNER/REPOSITORY.git (fetch)
> origin  https://github.com/OWNER/REPOSITORY.git (push)
```
### git remote set-url
- The git remote set-url command changes an existing remote repository URL.
```
The git remote set-url command takes two arguments:
    An existing remote name. For example, origin or upstream are two common choices.
$ git remote -v
> origin  git@github.com:OWNER/REPOSITORY.git (fetch)
> origin  git@github.com:OWNER/REPOSITORY.git (push)
git remote set-url origin https://github.com/OWNER/REPOSITORY.git
$ git remote -v
# Verify new remote URL
> origin  https://github.com/OWNER/REPOSITORY.git (fetch)
> origin  https://github.com/OWNER/REPOSITORY.git (push)
Use the git remote rename command to rename an existing remote.
The git remote rename command takes two arguments:
    An existing remote name, for example, origin
    A new name for the remote, for example, destinat
```
### git remote rm
```
$ git remote -v
# View current remotes
> origin  https://github.com/OWNER/REPOSITORY.git (fetch)
> origin  https://github.com/OWNER/REPOSITORY.git (push)
> destination  https://github.com/FORKER/REPOSITORY.git (fetch)
> destination  https://github.com/FORKER/REPOSITORY.git (push)
$ git remote rm destination
# Remove remote
$ git remote -v
# Verify it's gone
> origin  https://github.com/OWNER/REPOSITORY.git (fetch)
> origin  https://github.com/OWNER/REPOSITORY.git (push)
Note: git remote rm does not delete the remote repository from the server. It simply removes the remote and its references from your local repository.
```
- [ref](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)
### fetch -merge
```
These commands are very useful when interacting with a remote repository. clone and fetch download remote code from a repository's remote URL to your local computer, merge is used to merge different people's work together with yours, and pull is a combination of fetch and merge
```
### git clone
```
When you run git clone, the following actions occur:
    A new folder called repo is made
    It is initialized as a Git repository
    A remote named origin is created, pointing to the URL you cloned from
    All of the repository's files and commits are downloaded there
    The default branch is checked out
```
- git fetch origin :to fetch the origin content
- get merge main(the branch with what we want to merge the remote) origin/main(it is origin`/`main only )
- by these all files in the local which are not in remote are as well preserverd and new files which are in remote but not in local are downloaded
- but when coming to the point of modifications the remote repos modifications of a file will take precedence
### git pull
- to do the same(fetch and merge) in git pull for divergetn branches it says a lot
```
\home\radha\todo_list> git pull origin main
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 936 bytes | 936.00 KiB/s, done.
From https://github.com/m0wn1ka/todo_list_private
 branch            main       -> FETCH_HEAD
   ee1b46a..5c8d7f6  main       -> origin/main
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```
- [toread](https://git-scm.com/docs/user-manual)