# Version Control

| **Author(s)** | Vi Pham|
| :------------ | :-------------------------------------------------------------------------------------------- |
| **Reviewer(s)** | Quang Tran |
| **Start Date** | Nov 24th, 2020 |
| **Topic(s)** | General Techniques |
| **Status**       | In Progress |

# Index
- [Abstract](abstract)
- [Motivation](motivation)
- [Version Control Systems](version-control-sys)
- [Git Basics](git-basics)
- [Git Branching](git_branching)
- [7 Rules Of Great Git Commit Message](rules_git_commit_message)

## Abstract

## Motivation

## Version Control Systems (VCSs)

### Local Version Control Systems

Copy files into another directory, is easy to forget which directory you’re in and accidentally write to the wrong file or copy over files you don’t mean to.

To deal with this issue, programmers long ago developed local VCSs that had a simple database that kept all the changes to files under revision control.

![LVCS](/images/local.png)

One of the most popular VCS tools was a system called RCS, which is still distributed with many computers today. RCS works by keeping patch sets (that is, the differences between files) in a special format on disk; it can then re-create what any file looked like at any point in time by adding up all the patches.

### Centralized Version Control Systems

Need to collaborate with developers on other systems. To deal with this problem, Centralized Version Control Systems (CVCSs) were developed. These systems (such as CVS, Subversion, and Perforce) have a single server that contains all the versioned files, and a number of clients that check out files from that central place. 

![CVCS](/images/centralized.png)

If that server goes down for an hour, then during that hour nobody can collaborate at all or save versioned changes to anything they’re working on. If the hard disk the central database is on becomes corrupted, and proper backups haven’t been kept, you lose absolutely everything — the entire history of the project except whatever single snapshots people happen to have on their local machines. Local VCS systems suffer from this same problem — whenever you have the entire history of the project in a single place, you risk losing everything.

### Distributed Version Control Systems (DVCSs)

In a DVCS (such as Git, Mercurial, Bazaar or Darcs), clients don’t just check out the latest snapshot of the files; rather, they fully mirror the repository, including its full history. Thus, if any server dies, and these systems were collaborating via that server, any of the client repositories can be copied back up to the server to restore it. Every clone is really a full backup of all the data.

![DVCS](/images/distributed.png)

Furthermore, many of these systems deal pretty well with having several remote repositories they can work with, so you can collaborate with different groups of people in different ways simultaneously within the same project. This allows you to set up several types of workflows that aren’t possible in centralized systems, such as hierarchical models.

## Git Basics

### What is Git?

Git is a distributed version-control system for tracking changes in any set of files, originally designed for coordinating work among programmers cooperating on source code during software development. It goals include speed, data integrity, and support for distributed, non-linear workflows.

### Snapshots

Every time you commit, or save the state of your project, Git basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot. To be efficient, if files have not changed, Git doesn’t store the file again, just a link to the previous identical file it has already stored. Git thinks about its data more like a stream of snapshots.

![Snapshots](/images/snapshots.png)

### Commit

When you make a commit, Git stores a commit object that contains a pointer to the snapshot of the content you staged. This object also contains the author’s name and email address, the message that you typed, and pointers to the commit or commits that directly came before this commit (its parent or parents): zero parents for the initial commit, one parent for a normal commit, and multiple parents for a commit that results from a merge of two or more branches.

```
$ git add README test.rb LICENSE
$ git commit -m 'Initial commit'
```

## Git Branching

#### What is branch? 

A branch in Git is simply a lightweight movable pointer to one of these commits. The default branch name in Git is `master`. As you start making commits, you’re given a `master` branch that points to the last commit you made. Every time you commit, the `master` branch pointer moves forward automatically.

#### Create new branch

Create a new pointer for you to move around. Do this with the `git branch` command:
```
$ git branch testing
```
#### HEAD

The branch you are currently on, which is kept by a special pointer called `HEAD`.

#### Switch another branch

To switch to an existing branch.
```
$ git checkout testing
```
Shorthand for create a new branch and switch to it at the same time
```
$ git checkout -b sub_branch
Switched to a new branch sub_branch
```

#### Merge branches
#### Delete branch
### 2. Tag
### 3. Remote
#### Pull
#### Fetch
#### Push
# References
- [ ] Version control: Git Branching. [link](https://learngitbranching.js.org)
- [ ] Version control: 7 rules of great Git commit message. [link](https://chris.beams.io/posts/git-commit/)
- [ ] Trunk based development - a source-control branching model. [link](https://trunkbaseddevelopment.com)
