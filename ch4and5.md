# Chapter 4 and 5 Discussion



# Chapter 4 Making history
Need for storing relationships between commits in order to see a history.

## 4.1 The parent field

Each new commit after first has a `parent` field that contains ID of
previous commit.

Timestamps not viable. Sorting by time would require loaded all the
commits rather than doing linked list traversal. fetch/pull have similar
performance issues.

Git a distributed system where time might not be synchronized across
machines. Timestamps are metadata rather than core part of data model.

## 4.1.2 Differences between trees
Object IDs are derived from content.
New blobs are only created when content has changed.

## 4.2 Implementing the parent chain

## 4.2.1 Safely updating `.git/HEAD`

Files in `.git/objects` never change, but `.git/HEAD` does so the problem of
two processes writing to same file could be a problem for the latter.

For `.git/HEAD` and other references, writes must be atomic but can't use
the temp write and rename strategy.Subject to race conditions.

New abstraction called `Lockfile` to coordinate writes. The point is to
prevent two processes from getting access to same resource at once.

Prevents `.git/HEAD` from being inconsistently updated.

## 4.2.2 Concurrency and the file system

Why does this technique work?
The flags! `File::CREAT` and `File::EXCL` -- mirrors the interface provided
by C.

`0_CREAT` => file will be created if absent
`_EXCL` => call fails if file already exists

In C, all constants are defined globally.

Mutual exclusion works b/c telling the OS in one system call. Is single
atomic action from POV of user-space software.

If we checked for it ourselves, two concurrently running instances of
program could modify.

## 4.3 Don't overwrite objects
Small improvement!

Wasteful to write objects that already exist to disk.

# Chapter 5

## 5.1.1 File modes

`git cat-file below, HEAD^{tree}` ask Git for tree of the commit referenced
by `.git/HEAD`.

Numbers stored by Git are octal representation of the file's mode.

All files belong to a group. Group bits determine the permissions for
members of the file's group and the "other" bits determine the permissions
for everyone else.

Octal digits represent three bits of information.

Git only stores whether file is executable by owner. So just executables and
everything else.

## 5.1.2 Storing executables in trees

* not a real binary. True binaries contain machine code that can directly be
  executed by the operating system and hardware and don't require
  interpretation.

## 5.2.1 Recursive trees in Git

Subdirectories are listed using an Object ID that refers to another tree.

Merkle tree: method of storing a tree of information where each tree is
labeled with the hash of its children.

## 5.2.2 Building a Merkle tree

Git's tree objects must have entries sorted so it can tell if two entries
are the same.

Git sorts the files for the entire project before building the tree rather
than sorting entries within trees.

## 5.3 Reorganizing the project


