# Chapter 8 First-class commands

## 8.1 Repository class
- interface for getting Database, Index, Refs, and Workspace

## 8.2 Commands as classes
- make a wrapper
- take the input and instantiate a class to run

### 8.2.1 Injecting dependencies
- not a good idea to change local process state
- decouple from global references by passing arguments
- base class `Command::Base`
- throw `:exit` and catch it in base.

```ruby

def exit(status = 0)
  @status = status
  throw :exit
end
```

```ruby
def execute
  catch(:exit) { run }
end
```

executes the code in `run` up to the point that `exit` is called.

why dependency injection?
- removes implicit couplings
- isolate components from global environment
- fewer hidden assumptions


## 8.3 Testing the commands

- added a CommandHelper with shared methods
- changing the code w/ confidence

## 8.4 Refactoring the commands

# Chapter 9 Status report

Oh man, now the TDD comes into play.

## 9.1 Untracked files

Add test, add `tracked?` method to index for path name.
If untracked directory, diretory is listed as untracked rather than contents.
Check the @parents listing for updating the tracking.
If empty directory, outermost untracked directory still must appear in status output.

## 9.2 Index/workspace differences
- check Stat to compare file size and mode
- if not different, also hash the file and check what it would be, but don't
  store it in db
- timestamp optimization
  - don't read and hash file if timestamps match those stored in index
- deleted files
