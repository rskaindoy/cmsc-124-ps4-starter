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

- Which of its lines push a frame onto Activity 15's runtime stack? Which
  lines pop one?
- `Redo` resumes the goal's preserved execution state and executes the next untried clauses, searching for any potential matches and undoing variable bindings made previously, from whatever frame is currently at the top of the stack - which remained intact when it exited. A returned frame has already been popped from the stack, its memory was already deallocated and permanently lost and thus cannot resume from the last operation. It can be visually seen in the trace where we can see that `Redo` sits along the same level as the last `Exit`. 
- The difference is present in the subgoal order in the body of their recursive clause. `ancestor/2` is right recursive in both variants: it checks the knowledge base for the first match of an existing fact for `parent/2` first before it decides whether to run it on the recursive rule (short-circuiting). The same isn't true for `reach/2`, where one variant is left recursive: it attempts to evaluate the recursive rule first, which caused it to infinitely recurse by matching it with the first head it sees from the knowledge base each time it is called, and never even reaching the following subgoals until the stack overflows. The right recursive rule prevented it by short-circuiting an invalid match on the first subgoal, though it did end up with an infinte searching state instead (limited to this knowledge base where all edges connected as a cycle).
