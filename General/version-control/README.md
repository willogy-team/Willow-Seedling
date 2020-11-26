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

### Distributed Version Control Systems

In a DVCS (such as Git, Mercurial, Bazaar or Darcs), clients don’t just check out the latest snapshot of the files; rather, they fully mirror the repository, including its full history. Thus, if any server dies, and these systems were collaborating via that server, any of the client repositories can be copied back up to the server to restore it. Every clone is really a full backup of all the data.

![DVCS](/images/distributed.png)

Furthermore, many of these systems deal pretty well with having several remote repositories they can work with, so you can collaborate with different groups of people in different ways simultaneously within the same project. This allows you to set up several types of workflows that aren’t possible in centralized systems, such as hierarchical models.

## Git Branching

### 1. Commit, Branch
#### What is branch?
#### Types
#### Usage 
#### Create new branch
#### Switch another branch
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
