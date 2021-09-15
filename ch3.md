# Chapter 3

## 3.1 `init`

"wrapping data in typed object" => good idea
basic string manipulation, heh.
prefer working with structured data.

`Errno` => used for errors thrown by calls to OS

shell variable `$?` holds exit status of last command

- make .git repo
- make /objects and /refs

## 3.2 `commit`

> Recall that all objects are stored in the database by serialising them,
> and then prefixing the resulting string with the object’s type, a space,
> the length of the string, and a null byte

string might be written to disk all at once. programs often write to temp
location and then atomically move it to final destination.

"Z*H40" => special purpose language baked into Ruby

Array#pack => takes array and returns string representing those values. This
is cool.

## 3.2.3 Storing commits

commit contains pointer to a tree, info about author and committer and the
commit message.

Separate two commands by |, shell creates two processes to run in parallel

Objects!!!

- Use env vars for git attributes
- piping message in
- Store all the blobs in db
- Store the tree in db
- Store the commit in db
- Store commit oid in HEAD







