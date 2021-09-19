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
