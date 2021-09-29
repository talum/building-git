# Chapter 6 The Index

`add` and `index` provide cache of all blobs representing current state of
the project.

`index` is a staging area

## 6.2 Inspecting `.git/index`

4-byte version number? 2,3,4 are supported.
32-bit number of index entries

ctime: change time (contents or metadata changed)
mtime: modify time (contents changed)
dev: id of hardware device file resides on
ino: number of the inode storing attrs
mode: file mode

Time related values?? (I don't really see it)

info about file, file name, SHA

Use `add` to write latest version as a blob and store that blob's ID in the
index.

Old blobs aren't removed when index is updated. New blobs added to db, and
index points to different blobs.

`git ls-files --stage` lists all the files in index, also lists the file's mode and object ID

## 6.3 Basic `add` implementation

Index stores file modes as numbers rather than text.

End the file when the SHA-1 hash of its contents!

## 6.4 Storing multiple entries


# Chapter 7 Incremental change

Pessimistic locking for concurrency control (don't lose updates)

Why do we need the checksum? To verify contents didn't change while writing.
Makes sure the data we've read is not corrupt.

## 7.1

`add` reads from index data from `.git/index` on desk

## 7.2 Committing from the index

`commit` doesn't need to hash the project -- uses blob IDs cached in
`.git/index`

## 7.3 Stop making sense
Cache problems!
Fixing add to index so it discards existing entries that don't fit

## 7.3.1 Starting a test suite

Code to address edge cases, so write some tests

## 7.3.2 Replacing a file with a directory

Arrange, Act, Assert pattern for unit testing. Why don't we use this?

## 7.3.3 Replacing a directory with a file

Using multiple data structures to make lookups easier

## 7.4 Handling bad inputs
Raise error if files don't exist

## 7.4.2 Unreadable files

Unreadable file added to the database but blob is not in the index. Why?
What's the point?

## 7.4.3 Locked index file

What if locked file exists when invoked?

Example it gives is misleading? While commit command has editor open, index
is not actually locked. Legacy?






