# Chapter 25 Configuration

- mostly discussing the config file and the need to create and parse a file that's both human and machine readable -- tough!
- solution is to make a concrete syntax tree to preserve the extra content (comments)
- keys can be set via command line, and if they are, entire lines are replaced
- alternatively, human can modify the file themselves 

examples
- core editor
- name / email
- color formatting
- "mainline" in the sequencer options

## format
- section name
- subsection
- variable and value 

## concrete syntax tree
> To preserve as much of the original text as possible, a better approach is to parse it into a concrete structure that directly represents lines of text, but annotates each one with the machine- readable data it contains.
>  An abstract syntax tree (AST) distills a text down the the minimal structure necessary to extract its meaning, whereas a concrete syntax tree (CST) retains enough information to reconstruct the original text.

## modeling the config
- structs everywhere

## parsing the config file
- lock file
- read in memory and construct data structure
- hah nice regex 

## configuration stack
- local
- gloabl
- system files 
- the composite pattern where they're all treated as ONE
- (this def used to confuse me) 

### Questions
1. Was anyone else surprised that this wasn't boring?!
2. Did anything surprise you about config files? If so, what? 
3. Did you learn anything new about the many configuration files that exist?
4. Has anyone used the composite pattern before? 
