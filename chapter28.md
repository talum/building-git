# Chapter 28 Fetching content

- Fetching: downloading objects & updating remote's refs/heads pointers into refs/remotes directory


## 28.1 Pack negotiation
- only send objects receiver does not already have
- example with alice: good reminder there are any number of remotes you could fetch from, not necessarily one central one 
- `upload-pack` sends back list of all refs and what they point at
- client sends commit IDs it wants, then flush packet
- server sends list of commits that its refs point at followed by message "done"
- if someone has a certain commit, they have everything that commit points to -- yep this is nice
- need to send all the missing commits

### 28.1.1 Non-fast-forward updates
- send the full list of have commits so that fewer objects need to be transferred
- `multi_ack` is supported by `upload-pack` so client can send batches of commits. server just needs to find a common ancestor
- Git sends commits in blocks of 32 (see Git documentation)


## 28.2 The `fetch` and `upload-pack` commands
- overview of the process
- reasonable defaults, defaults to origin

### 28.2.1 Connecting to the remote
- interesting choice to make it work with repos on same machine
- use of Shellwords module

### 28.2.2 Transferring references
- get all references from `list_all_refs`
- nice code reuse, it's like he knew what was going to happen
- client stores remote refs in a hash

### 28.2.3 Negotiating the pack
- server sends refs
- client sends whole history -- no optimization in this version
- optimal pack will still be generated

### 28.2.4 Sending object packs
- interesting writing technique...step by step from client to server gets a little confusing
- kind of hard to illustrate the back and forth here
- save packed objects to local db 
- 
### 28.2.5 Updating remote refs
- update the text output 

### 28.2.6 Connecting to remote repositories
- run program on remote with SSH to get access to I/O
- use Shellwords library

## 28.3 Clone and pull
- eventual consistency over state of project

### 28.3.1 Pulling and rebasing
- good if you want a linear history
- reset to other branch, fast forward own 
- do a cherry-pick
- 
### 28.3.2 Historic disagreement
- removing content can get hard
- might re-add content you intended to delete due to merge
- better to revert 

Delayed: I finally get why refspecs are useful. For instance, can use a namespace to only fetch those branches I care about.

## Questions ??? 
