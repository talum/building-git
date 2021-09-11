# Chapter 2

## 2.1 The `.git` directory

### 2.1.1 `.git/config`

configuration settings just for this repo, not for overall Git usage

### 2.1.2. `.git/description`

name of the repo

### 2.1.3 `.git/HEAD`

contains a reference to the current commit (commit ID or a symbolic reference)

commit referenced by HEAD becomes new commit's parent.

### 2.1.4 `.git/info`

contains metadata

`.git/info/exclude` vs `.gitignore` => latter is part of source tree.
`exclude` file remains just on your machine

### 2.1.5 `.git/hooks`

scripts for Git to execute

### 2.1.6 `.git/objects`

Git's database for storing tracked content

`.git/objects/pack` for storing objects in optimized format. Loose objects
turned into a pack: single file w/ many objects in compressed format.

`.git/objects/info` stores metadata about packs.

### 2.1.7 `.git/refs`

`refs` stores pointers into the `.git/objects` db.

## 2.2 A simple commit

Root commit is a commit with no parents.

### 2.2.1 `.git/COMMIT_EDITMSG`

Used to compose commit messages

### 2.2.2 `.git/index`
contains binary data
cache that stores info about each file in current commit

### 2.2.3 `.git/logs`
contain a lot of every time a ref changes
used by `reflog` command

### 2.2.4 `.git/refs/heads/master`
records which commit is at tip of `master`

## 2.3 Storing objects

### 2.3.1 `cat-file`

show object from git db: `git cat-file -p <ID of object>`

`tree`: whole tree of files as they were when commit was made. one tree for
every subdirectory in project. each entry in tree is either another tree or
a blob.

mode of a file: numeric representation of its type and permissions.

Git stores blobs' literal contents.

### 2.3.2 Blobs on disk

Git tries to compress every object it stores. DEFLATE compression algo with
zlib.

Git stores blobs by prepending w/ `blob` space length and null byte, then
compressing with zlib.

### 2.3.3 Trees on disk
Git stores ID of each entry in packed format, 20 bytes for each one.

Object IDs are hexadecimal representations of numbers.

160-bit object ID is stored in binary as 20 bytes.


### 2.3.4 Commits on disk

Commits stored as series of headers followed by message.

| tree: All commits refer to a single tree that represents the state of your files at that point in the history. Git stores commits as pointers to a complete snapshot of the state of your project, rather than storing diffs between versions.

author: metadata

committer: metadata. usually same as author but differ when someone else amends the commit or cherry-picks. time reflects time at commit rather htan authoring.

### 2.3.5 Computing object IDs

SHA-1 hash function. 160 bits = 20 bytes = 40-digit hex representation

2^160 possible object IDs. computationally infeasible to find a collision.

To get the object ID: take content, add type and length prefix, hash it.
This happens before compression.

If two objects have same ID, they must have same content (to extent
guaranteed by SHA-1). Saves time on diffing and synchronization.

### 2.3.6 Problems with SHA-1

## 2.4 The bare essentials







