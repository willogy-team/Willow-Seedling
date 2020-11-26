# Version Control

| **Author(s)** | Vi Pham|
| :------------ | :-------------------------------------------------------------------------------------------- |
| **Reviewer(s)** | Quang Tran |
| **Start Date** | Nov 24th, 2020 |
| **Topic(s)** | General Techniques |
| **Status**       | In Progress |

# Index
- [Abstract](abstract)
- [Motivation / Version Control Systems](motivation-vc-system)
- [Git Basics](git-basics)
- [Git Branching](git_branching)
- [Git Commit Message](git_commit_message)

## Abstract

Version Control is a class of systems responsible for managing changes to computer programs, documents, large web sites, or other collections of information. Git is a special system to speed, data integrity, and support for distributed, non-linear workflows.

## Motivation / Version Control Systems (VCSs)

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

### Tag

Git has the ability to tag specific points in a repository’s history as being important. Typically, people use this functionality to mark release points (`v1.0`, `v2.0` and so on). In this section, you’ll learn how to list existing tags, how to create and delete tags, and what the different types of tags are.

List tag:
```
$ git tag
v1.0
v2.0
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
#### Branching

After some commits with two different branch:
![Branching](/images/basic-branching.png)

#### Merge branches

Have to do is check out the branch you wish to merge into and then run the git merge command:

```
$ git checkout master
Switched to branch 'master'
$ git merge iss53
Merge made by the 'recursive' strategy.
index.html |    1 +
1 file changed, 1 insertion(+)
```
![Merge1](/images/basic-merging-1.png)

Instead of just moving the branch pointer forward, Git creates a new snapshot that results from this three-way merge and automatically creates a new commit that points to it. This is referred to as a merge commit, and is special in that it has more than one parent.

![Merge2](/images/basic-merging-2.png)

#### Delete branch

Have no further need for the iss53 branch. You can close the issue in your issue-tracking system, and delete the branch:

```
$ git branch -d iss53
```
#### Rebase
The second way to integrate changes from one branch into another ( the first way: `merge`). With the `rebase` command, you can take all the changes that were committed on one branch and replay them on a different branch.

```
$ git checkout experiment
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: added staged command
```

![rebase](/images/basic-rebase-3.png)

#### Remote

Remote references are references (pointers) in your remote repositories, including branches, tags, and so on. You can get a full list of remote references explicitly with `git ls-remote <remote>`, or `git remote show <remote>` for remote branches as well as more information. 

##### Push

Want to share a branch with the team, you need to push it up to a remote to which you have write access.

```
$ git push origin <branch>
```

##### Pull

Get a branch from server to your working directory.

```
$ git pull origin <branch>
```

## Git Commit Message

### Why is good commit messages

How to you find one commit with messages too few informations. 
Smoothly, all team member can communicate context about changes

### Rules

- Separate subject from body with a blank line

```
Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequences of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```

- Limit the subject line to 50 characters

> So shoot for 50 characters, but consider 72 the hard limit.

- Capitalize the subject line

> For example:<br/>
> - Accelerate to 88 miles per hour<br/>
> Instead of:<br/>
> - accelerate to 88 miles per hour

- Do not end the subject line with a period

> For example:<br/>
> - Open the pod bay doors<br/>
> Instead of:<br/>
> - Open the pod bay doors.

- Use the imperative mood in the subject line

- Wrap the body at 72 characters

- Use the body to explain what and why vs. how

# References
- [ ] Version control: Git Branching. [link](https://learngitbranching.js.org)
- [ ] Version control: 7 rules of great Git commit message. [link](https://chris.beams.io/posts/git-commit/)
- [ ] Trunk based development - a source-control branching model. [link](https://trunkbaseddevelopment.com)
- [ ] Git Documentation. [link](https://git-scm.com/doc)
