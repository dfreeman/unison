# Empty namespace behaviours

```unison
mynamespace.x = 1
```

The deleted namespace shouldn't appear in `ls` output.
```ucm
.> ls

  nothing to show

```
```ucm
.> ls.verbose

  😶
  
  No results. Check your spelling, or try using tab completion
  to supply command arguments.
  
  `find.global` can be used to search outside the current
  namespace.

```
```ucm
.> find mynamespace

  😶
  
  No results. Check your spelling, or try using tab completion
  to supply command arguments.
  
  `find.global` can be used to search outside the current
  namespace.

```
## history

The history of the namespace should still exist if requested explicitly.

```ucm
.> history mynamespace

  Note: The most recent namespace hash is immediately below this
        message.
  
  ⊙ 1. #nvh8d4j0fm
  
    - Deletes:
    
      x
  
  □ 2. #i52j9fd57b (start of history)

```
Merging an empty namespace should still copy its history if it has some.

```ucm
  ☝️  The namespace .empty is empty.

.empty> history

  ☝️  The namespace .empty is empty.

.empty> merge .mynamespace

  Nothing changed as a result of the merge.

.empty> history

  Note: The most recent namespace hash is immediately below this
        message.
  
  ⊙ 1. #nvh8d4j0fm
  
    - Deletes:
    
      x
  
  □ 2. #i52j9fd57b (start of history)

```
Add and then delete a term to add some history to a deleted namespace.

```unison
deleted.x = 1
stuff.thing = 2
```

## fork

I should be allowed to fork over a deleted namespace

```ucm
.> fork stuff deleted

  Done.

```
The history from the `deleted` namespace should have been overwritten by the history from `stuff`.

```ucm
.> history stuff

  Note: The most recent namespace hash is immediately below this
        message.
  
  
  
  □ 1. #q2dq4tsno1 (start of history)

.> history deleted

  Note: The most recent namespace hash is immediately below this
        message.
  
  
  
  □ 1. #q2dq4tsno1 (start of history)

```
## move.namespace

```unison
moveoverme.x = 1
moveme.y = 2
```

I should be able to move a namespace over-top of a deleted namespace.
The history should be that of the moved namespace.

```ucm
.> delete.namespace moveoverme

  Done.

.> history moveme

  Note: The most recent namespace hash is immediately below this
        message.
  
  
  
  □ 1. #c5uisu4kll (start of history)

.> move.namespace moveme moveoverme

  Done.

.> history moveoverme

  Note: The most recent namespace hash is immediately below this
        message.
  
  
  
  □ 1. #c5uisu4kll (start of history)

```
