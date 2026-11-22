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

- Which of its lines push a frame onto Activity 15's runtime stack? Which
  lines pop one?
- What does a `Redo` line resume that a returned frame cannot?
- Why does swapping the two clauses of `reach/2` change whether the search
  ever answers, while swapping the two clauses of `ancestor/2` only changes
  the order of the answers?
