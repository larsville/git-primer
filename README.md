### git-primer

Notes to myself about learning Git. This is not a tutorial. It is a self-contained introduction to the basic concepts, with pointers to more information useful to beginners.

## Background:

I first tried learning Git and GitHub by immersion on a real project with a team of remote people. I knew Git was "different" and that I'd need to unlearn various concepts and terminology from other source code management systems. I found that even good authors and astute colleagues sometimes wrote or spoke in a loose or inconsistent way that made it easy for a beginner to take a mental wrong turn. I was able to limp along, but at best I always needed a lot of help, and I never really felt like I knew what I was doing.

So I decided to start again from the ground up, getting solid on the underlying concepts and terminology before getting my hands too dirty. I read a lot, and took notes, documenting these concepts in my own words. This worked a lot better for me. Maybe this cleaned-up and expanded version of my notes will be helpful to you. If you find issues, let me know. I try to assume as little as possible about what you know.

I've highlighted things that I had to unlearn, or insert into my brain with special care, as __Mental floss__.

## What are Git and GitHub?

_[Git](https://en.wikipedia.org/wiki/Git)_ is a software program that keeps track of changes to a project over time. (Technically, it is a "distributed version control system", or DVCS.)

To Git users, a project is simply a folder and its contents, including any subfolders and their contents, and so on. Most projects managed by Git contain files of software code, but people also use Git to manage things like artwork files, documentation files, etc. A project folder can also contain files that aren't managed/tracked by Git, such as log files or other incidental material. Git ignores such files.

Git is command-line software, and it is somewhat complex as these things go, so it is hard for many people to learn. A good way to get started with Git is to use _[GitHub](https://github.com)_, which is a web site that supplies a web interface for most Git functionality. Many people find this much easier to use than the command line, especially for the most common operations. Many GitHub users find that they never need to use Git directly. Still, it is essential to understand the basic Git concepts.

GitHub also provides project storage, comprising millions of public and private projects. GitHub also provides other collaboration functionality such as bug tracking and wikis for each project.

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

To make a change, a team member edits the files on his local clone repository, and/or creates new files. The team member then adds the changed & new files to a list in the local clone repository, using the `git add` command, which automatically figures out which files are changed & new. This list is called the _staging area_ or _index_. Once all desired changes are made, the team member documents the changes in the local clone repository using the `git commit` command. Committing changes to the staging area is one of the most frequently used Git operations.

__Mental floss__: "origin" means the repo that a clone was cloned from, but "original" often refers to the upstream repo; i.e. the one that is original to the project.

__Mental floss__: "fork" is not a Git command; it is a GitHub command that supports the common "fork and pull" workflow. Colloquially, a "fork" is a clone of a repository.

__Mental floss__: Adding a file doesn't mean adding it to the set of files managed by Git. It means adding it to the staging area for the next commit. You might "add" the same file many times before committing the accumulated changes. Also, committing doesn't mean merging changes into a "master" repository somewhere. It means recording them in your local staging area. Merging changes committed in one repository to another repository is done via a pull or push, which might encompass many commits. Note that commit can be a verb (the act of committing), or a noun (the resulting record of changes).]

After the commit, the local clone repository has recorded all the changes, and the user can continue to do more work without affecting that commit. But that doesn't do the team any good until the changes are submitted back to the original repository. To do this, the team member who made the changes can issue a pull request. This notifies the owner(s) of the original repository that someone wishes to submit work that is recorded in a commit. The owner(s) of the original repository can review the changes, reject them, ask for more information, or accept them. (Specific team members might be listed as contributors to the original repository. In that case, they can push their changes directly to the original repository, bypassing the pull request process.)

Once the changes are merged, other team members can update their own local clone repositories from the original repository. Team members can do further edits and commits, or they can delete their local repositories, since the network repository will have a record of everything that was done. With Git, each repository has a record of all changes to all project files, even if it no longer has access to the machine on which the changes were done.

## What is Github Gist?

_[Gist](https://gist.github.com)_ is a web site run by GitHub, designed for simple Git projects comprising snippets of text or code. It is similar to a _[pastebin](https://en.wikipedia.org/wiki/Pastebin)_, with each gist having its own Git repository.

## Terms & Concepts:

A _repository_ is a set of files (usually source code) that makes up a project, stored on a Git server (such as GitHub).

A _bare_ or _shared_ repository is a special kind of repository that doesn't have a working directory. This is the standard way to start a project that many people will work on. [  ] needs more

A _fork_ is a copy of a repository that remembers the repository it is a copy of (called the upstream repository), so that changes to the fork can later be merged back into that repository, and vice versa (using a pull request). You might think that this copy lives on your machine, but it doesn't until you clone it. In fact, saying that a fork is a copy is taking a liberty -- it is more like a declaration of intent to make a copy of the files.
[ ] is a fork just a (special?) repository? Is it anything at all in Git? It is a control in GitHub, but there is no "fork" command in Git, you just clone something. Maybe cloning on the server = forking or branching, cloning on the desktop = "cloning".

A _clone_ of a repository is a copy of the repository files on your computer. You clone a repository (usually a fork of another repository) so that you can make changes to its files, or to use it as the starting point for a new project.

A _branch_ is similar to a fork, but it happens on the server side instead of the client side. Only registered collaborators on a project can create a branch. The branch becomes another remote for the project. A branch is a pointer to a commit. Branches have labels. Every branch has a default label called Master, which always points to the latest commit for that branch. 

A _pull request_ is the way to tell the owner of a repository that you have some code that you think should be merged into it. (I suppose the name means that you are requesting that the repository owner pull your code into his.)

_Syncing_ a clone/branch/fork is updating it with the latest stuff in its upstream repository. This does not modify any project files on the server.

__Mental floss__: In many systems, "sync" means to send changes back and forth. In Git, syncing is a one-way operation.

[ ] what happens to files with differences?
[ ] to sync, you must first "configure an upstream remote". WTF? Also, do you have to do this every time you sync?

_Remote_ [URL] - a repository where files are stored; could be a repository on GitHub, or a different server, or a fork. Remotes have names. Your default remote is usually called "origin". Use "git remote -v" to list remote short names/handles and URLs. Use "git remote add" to associate a remote with a name.
_Origin_ - what your default remote for a project is usually called -- it is the "origin" that your code will be pulled toward.
_Upstream_

_Commit_ -- copies changes in staged files to a remote repository. (Also launches your default editor ($EDITOR) with some default commit comment text. When you exit the editor, comment lies are stripped out. Or use git commit -m "comment".) As a noun, a commit is a snapshot of the Tracked files in your working directory.
_Push_ -- pushes commits made on your local branch to a remote repository
_Fetch_ -- do this before you can push local changes (does this apply only to branches, or to forks as well?)
_Merge_ -- do this before you can push local changes (does this apply only to branches, or to forks as well?)

_Upstream_ -- the repository that a fork was made from is the upstream repository.

_Index_ or _staging area_ is a file (in the working directory?) that contains info about what will go into your next commit

_Add_ -- adds a file to the next commit, (which can also add it to the project; i.e. make it Tracked. Or use `git commit -a -m "comment"` to skip the separate add step; this will automatically stage every tracked file before committing it.)
_Checkout_ -- restores a Modified file (Staged or Unstaged) to its state as of last commit. (Not undoable!)

_Init_ -- creates a repository, either local (in the directory you specify) or remote (by running it on a server). This is how you create a repository from scratch. Most repositories are created by cloning instead.

_Working directory_ -- the folder tree where you have content that you want to manage with Git. A bare repository has only metadata, and no working directory, and is customarily used as a central repository to be shared by a team. A non-bare repository has a .git folder to store Git metadata.

_Tracked_ -- a file on your local machine is "tracked" if Git knows about it. Otherwise it is untracked. Adding a file causes it to be tracked and staged. Removing a modified file causes it to be untracked. [ ] Can you remove a modified or staged file?

_Unmodified_ / _Modified_ / _Staged_ -- a tracked file is in one of these states. Editing an Unmodified file causes it to become Modified. Adding a Modified file causes it to become Staged. Committing a Staged file causes it to become Unmodified.

_Rebase_ [ ] tbd

__Mental floss__: A file can be both staged and unstaged at the same time! If you modify it and then add it, it will become staged, and if you then modify it again, there will be a staged version and an unstaged version. Adding it again will stage the most recently edited version and vaporize the previously staged version.

`git diff` shows changes in modified but unstaged files.
`git diff --staged` or `git diff --cached` shows changes in staged files.

__Tip__: commit all staged files before merge or checkout

## Basic Workflow: Making changes to a project

* Find a repository that interests you. Maybe you want to submit a fix for it, or maybe you want to use it as a starting point for another project. Let's assume the former for now.
* Fork the project.
* Clone the fork to create copies your local machine.
* Make whatever changes you want to the clone on your local machine.
* Create a pull request so that other collaborators can review the changes in your fork.
* [ ] finish this


## Basic Workflow: Using a project as a template for a new project

* [ ] finish this

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
