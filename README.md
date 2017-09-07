### Git Primer

Copyright (c) 2016 Lars Jensen

This file is meant to help you start learning Git and GitHub. It is not a tutorial. It is an introduction to the basic concepts and terminology, with pointers to more information that might be especially useful to beginners. It aims to give readers a solid mental foundation by being clear, concise, correct, and unambiguous.

## Background

I first tried learning Git and GitHub by immersion on a real project with a team of remote people. I knew Git was "different" and that I'd need to unlearn various concepts and terminology from other source code management systems. I found that even good authors and astute colleagues sometimes write or speak in a loose or inconsistent way that makes it easy for a beginner to take a mental wrong turn. I was able to limp along, but I always needed a lot of help, and I never really felt like I knew what I was doing.

So I decided to start again from the ground up, getting clear on the underlying concepts and terminology before getting my hands too dirty. I read a lot, and took notes, documenting these concepts in my own words. This approach worked a lot better for me. Maybe this cleaned-up and expanded version of my notes will be helpful to you. I try to assume as little as possible about what you know. If you find issues, let me know.

I've highlighted things that I had to unlearn, or insert into my brain with special care, as __Mental floss__.

## What are Git and GitHub?

_[Git](https://en.wikipedia.org/wiki/Git)_ is a software program that keeps track of changes to a project over time. (Technically, it is a "distributed version control system", or DVCS.)

To Git users, a "project" is simply a folder and its contents, including any subfolders and their contents, and so on. Most projects managed by Git contain files of software code, but people also use Git to manage things like artwork files, documentation files, etc. A project folder can also contain files that aren't managed/tracked by Git, such as log files or other incidental material. Git ignores such files.

Git is [command-line software](https://en.wikipedia.org/wiki/Command-line_interface), and it is somewhat complex as these things go, so it is hard for many people to learn. A good way to get started with Git is to use _[GitHub](https://github.com)_, which is a web site that supplies a web interface for most Git functionality. Many people find the GitHub web site to be much easier to use than Git as a command line tool, especially for the most common operations. A GitHub user might never need to use Git directly. Even so, it is essential to understand the basic Git concepts and terminology.

GitHub also provides project storage, comprising millions of public and private projects. GitHub also offers other collaboration functionality for each project, such as bug tracking and [wikis](https://en.wikipedia.org/wiki/Wiki).

## How does Git work?

Git stores its data in a _repository_, or _repo_ for short. A Git repository is stored in the top level of the project folder, right alongside the project files and subfolders, in a special repository subfolder named `.git`. The repository subfolder contains, among other things, a record of every change to every file in the project since Git started managing the project.

There is only one repository subfolder per project, regardless of how many subfolders the project has. (Some other version control systems maintain file-tracking info in each subfolder of a project.) Most users don't need to know how the repository subfolder itself is organized. You might never even see the repository subfolder, because items whose names start with a period are typically hidden from view.

__Mental floss__: Sometimes authors use "repository" to mean the entire project folder, including the `.git` repository subfolder, and sometimes it means the just the `.git` subfolder. Don't confuse the two usages.

Here are some times when it makes sense to create a repository:

* starting a new project just for yourself, on your local drive
* starting a new project for your team on a network drive or web site (like GitHub).
* copying a repository as a way to make changes to a project (a.k.a. _cloning_ or _forking_ or _branching_)
* copying a repository as a way to start a new project

Git can be useful for tracking changes to projects that only one person works on, but the main use of Git is to allow a team of people to work on the same project. There are several ways to do this. A common way is for the team to create a new repository on a network drive (using the `git init` command), make it accessible to all team members, and then each team member copies the repository to his own computer using the `git clone` command. The _clone_ repository remembers which repository it was cloned from. That repository is called the clone's _origin_. Team members routinely update their local clone repositories from the origin, to reduce the chance of conflicts when merging their changes later.

__Mental floss__: "origin" means the repo that a clone was cloned from, but "original" often refers to the most upstream repo; i.e. the one that is original to the project.

To make a change, a team member edits the files on his local clone repository, and/or creates new files. The team member then records the changes & new files in a list in the local clone repository. This list is called the _staging area_ or _index_. Changes are recorded in the staging area using the `git add` command, which automatically figures out which files are changed & new. Once all desired changes are made, the team member documents the changes in the local clone repository using the `git commit` command. Committing changes in the staging area is one of the most frequent Git operations.

__Mental floss__: Adding a file does _not_ mean adding it to the set of files managed by Git. It means adding changes made to that file to the staging area for the next commit operation. You might "add" the same file many times before "committing" the accumulated changes.

__Mental floss__: Committing does _not_ mean merging changes into a "master" repository somewhere. It means recording them (usually with comments) in your local repository from the staging area, and then emptying the staging area. Merging changes committed in one repository to another repository is done via a pull or push, which might encompass many commits. Note that commit can be a verb (the act of committing), or a noun (the resulting record of changes).

After the commit, the local clone repository has recorded all the changes, and the user can continue to do more work without affecting that commit. But that doesn't do the team any good until the changes are submitted back to the original repository. To do this, the team member who made the changes can issue a _pull request_. This notifies the owner(s) of the original repository that someone wishes to submit work that is recorded in a commit. The owner(s) of the original repository can review the changes, reject them, ask for more information, or accept them. (Specific team members might be listed as _contributors_ to the original repository. In that case, they can push their changes directly to the original repository, bypassing the pull request procedure.)

Once the changes are merged, other team members can update their own local clone repositories from the original repository. Team members can do further edits and commits, or they can delete their local repositories, since the original repository will have a record of everything that was done. In fact, with Git, each repository has a record of all changes to all project files, even if it no longer has access to the machine on which the changes were done.

## What is Github Gist?

_[Gist](https://gist.github.com)_ is a web site run by GitHub, designed for simple Git projects that consist of a small number of files, or a single file or snippet. Gist is similar to a _[pastebin](https://en.wikipedia.org/wiki/Pastebin)_, with each gist having its own Git repository. Such repositories are also called gists.

## Terms & concepts: Working with repositories

A _repository_ is a set of files (usually source code) that makes up a project, stored on a Git server (such as GitHub).

_`init`_ -- creates a repository, either local (in the directory you specify) or remote (by running it on a server). This is how you create a repository from scratch. Most repositories are created by cloning instead.

A repository's _working directory_ is the folder (including subfolders) that contains its project files and its `.git` subfolder. A _bare_ or _shared_ repository has only the  `.git` subfolder, and thus no working directory, and is customarily used as a central repository to be shared by a team. [tbd: why?]

A _clone_ is a copy of a repository that remembers the repository it is a copy of (called the _upstream_ repository), so that changes to the clone can later be merged back into that repository (using a _pull request_), or vice versa (using `sync`).

A _fork_ of a repository is a clone of that repository. __Mental floss__: This is among the most confusing parts of learning Git. Git has no "fork" command; GitHub added the "fork" operation to make collaboration easier by automating the common "fork and pull request" workflow. A typical workflow for making changes to a project is that you "fork" the project's "master" repository on the server (thus creating a copy of the master in your account so that you can modify it), and then "clone" a copy of the fork on your local machine (where you can make changes and test them out). The fork and the clone are both repositories, each remembering its immediate parent. The word "fork" can refer to a copy of a repository on a server, or to a local clone of that copy, or to both, or to the act of creating them.

A _branch_ is similar to a fork, but it happens within a repository instead of creating a new repository. Only registered collaborators on a project can create a branch. A branch is a pointer to a commit. The branch becomes another remote for the project. Branches have labels. Every branch has a default label called `master`, which always points to the latest commit for that branch. [tbd: check all this]

A _pull request_ is the way to tell the owner of a repository that you have some code that you think should be merged into the repository. In other words, you are requesting that the repository owner accept your changes by "pulling" them into his project; you are not allowed to "push" your changes into someone else's repository.

To _sync_ a clone/branch/fork is to update it with the latest stuff from a _remote_ repository, usually its _upstream_ remote, which is normally named _`origin`_. This does not modify any project files on the server. __Mental floss__: In many systems, "sync" means to send changes back and forth. In Git, syncing is a one-way operation. [tbd: what actually happens to files with differences?]

An _upstream_ repository is the one that a clone was copied from.

A _remote_ for a project is a repository specified as a named URL. A remote can point to a repository on GitHub, or on a different server, or a local repository. A project can have several remotes, or none. The default remote for a project is the repository that the project was cloned from, and it is normally named _`origin`_. Use `git remote -v` to list a project's remotes. Use `git remote add` to associate a remote URL with a name.

_`Origin`_ is the standard name for the default remote for a project. The default remote is the repository that your code will be merged with if someone acts on your pull request.

## Terms & concepts: Working with files

_Commit_ -- copies changes in staged files to a repository. (Also launches your default editor ($EDITOR) with some default commit comment text. When you exit the editor, comment lines are stripped out. Or use `git commit -m "comment"`.) As a noun, a commit is a snapshot of the Tracked files in your working directory.

_Push_ -- pushes commits made on your local branch to a remote repository [tbd: explain vs pull]

_Fetch_ -- do this before you can push local changes [tbd: does this apply only to branches, or to clones as well?]

_Merge_ -- do this before you can push local changes [tbd: does this apply only to branches, or to clones as well?]

A project's _index_ or _staging area_ is a list that contains info about what will go into the next commit for that project.

_Add_ -- adds a file to the next commit. This might also add the file to the project; i.e. make it _tracked_. Or use `git commit -a -m "comment"` to skip the separate add step; this will automatically stage every tracked file before committing it.)

_Checkout_ -- restores a `modified` file (whether `staged` or `unstaged`) to its state as of the last commit. Note the checkout is not undoable! __Mental floss__: This is vastly different from what "checkout" means in some version control systems, i.e. to unlock a local copy of a file so that you can edit it.

A file in a repository is _tracked_ if Git knows about it. Otherwise it is _untracked_. Adding a file causes it to be tracked and staged. Removing a modified file causes it to be untracked. [tbd: can you remove a modified or staged file?]

A _tracked_ file is in one of these states: _unmodified_ / _modified_ / _staged_. Editing an unmodified file causes it to become modified. Adding a modified file causes it to become staged. Committing a staged file causes it to become unmodified.

__Mental floss__: A file can be both _staged_ and _unstaged_ at the same time! If you modify it and then add it, it will become _staged_, and if you then modify it again, there will be a _staged_ version and an _unstaged_ version. Adding it again will stage the most recently edited version and vaporize the previously _staged_ version.

`git diff` shows changes in _modified_ but _unstaged_ files.
`git diff --staged` or `git diff --cached` shows changes in _unstaged_ files.

__Tip__: commit all staged files before merge or checkout [tbd: explain]

_Rebase_ [tbd: add]

## Basic Workflow: Make changes to a project

1. Find a repository that interests you. (Maybe you want to submit a fix for it, or maybe you want to use it as a starting point for another project. We'll assume the former.)
2. Use GitHub to fork the project, which creates a copy of the project in your account on the GitHub server.
3. Clone the fork, which creates a copy of the project on your local machine.
4. Make whatever changes you want to the clone on your local machine.
5. Create a pull request so that the owner of the original project can review the changes you made.
6. [tbd: finish]


## Basic Workflow: Use a project as a template for a new project

* [tbd: finish]

## Basic Workflow: Experiment with some ideas, and then abandon them

* [tbd: finish]

## Good sources that helped me solidify my understanding:

_Atlassian Git Tutorial_ - One of the best tutorials. Detailed, lengthy, clean, well written.  
https://www.atlassian.com/git/tutorials/  

_Pro Git_ - A very popular, comprehensive reference. The Git bible, for many. I don't personally recommend it as a tutorial because I think it tends to introduce new terms without defining them well enough, and I find the language to be a bit loose.  
https://git-scm.com/book/en/v2

_Understanding Git Conceptually_ - A tutorial that builds understanding starting with the data model, an approach I like. A bit abstract and technical in spots, but precisely and concisely written. I used it to spot-clean mental stains left in my brain by less fastidious authors.  
https://www.sbf5.com/~cduan/technical/git/

_Scott Lowe_ - Very good tutorial pages with a lot of explanatory detail and clear, relatively non-technical writing.  
http://blog.scottlowe.org/2015/01/14/non-programmer-git-intro/  
http://blog.scottlowe.org/2015/01/26/using-git-with-github/  
http://blog.scottlowe.org/2015/01/27/using-fork-branch-git-workflow/  

_Bryan Pendleton_ - Good discussion of forking vs cloning. Summary: They both copy a repo, but you fork on the server, and clone the fork locally. Work in the clone, push/pull to the fork to show others your work.  
http://bryanpendleton.blogspot.com/2014/07/git-clone-vs-fork.html

_Jon Saints_ - Good discussion of bare repositories. Summary: They are the usual way to implement a central repo.  
http://www.saintsjd.com/2011/01/what-is-a-bare-git-repository/

_Steve Bennet_ - Instructive list of several Git downsides, including a great diagram that serves as a nice cheat sheet (even as it indicts Git's command complexity).  
http://stevebennett.me/2012/02/24/10-things-i-hate-about-git/

_Pieter Hintjens_ - "Git Branches Considered Harmful" argues for always forking, never branching.  
http://hintjens.com/blog:24
