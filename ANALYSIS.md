# The Search and the Stack

## Trace (P07)

```
== trace P07 ==        
Call: grandparent(tom,X)
 Call: parent(tom,_)
 Exit: parent(tom,liz)
 Call: parent(liz,X)
 Fail: parent(liz,X)
 Redo: parent(tom,liz)
 Exit: parent(tom,bob)
 Call: parent(bob,X)
 Exit: parent(bob,ann)
Exit: grandparent(tom,ann)
answer 1: X=ann
Redo: grandparent(tom,ann)
 Redo: parent(bob,ann)
 Exit: parent(bob,pat)
Exit: grandparent(tom,pat)
answer 2: X=pat
Redo: grandparent(tom,pat)
 Redo: parent(bob,pat)
 Fail: parent(bob,X)
 Redo: parent(tom,bob)
 Fail: parent(tom,_)
Fail: grandparent(tom,X)
== 2 answers ==
```

## Q1
Every Call line pushes a frame. Line 2 pushes grandparent(tom,X), and lines 3, 5, and 9 push the parent goals one level deeper, which the indentation shows. Every Exit or Fail line pops a frame and returns to the caller. Line 4 pops parent(tom,liz) with a result, line 6 pops parent(liz,X) with nothing, and line 11 pops grandparent(tom,ann). The last pop is the Fail on line 23, when grandparent(tom,X) has no answers left. Redo lines (7, 13, 14, 18, 19, and 21) are neither, since they only resume a goal that already exited.

- What does a `Redo` line resume that a returned frame cannot?
- Why does swapping the two clauses of `reach/2` change whether the search
  ever answers, while swapping the two clauses of `ancestor/2` only changes
  the order of the answers?
