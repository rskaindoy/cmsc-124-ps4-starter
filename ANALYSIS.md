# The Search and the Stack

Replace this paragraph after your checks pass. Paste the output of `./trace`
for one case. Then answer three questions about it.

- Which of its lines push a frame onto Activity 15's runtime stack? Which
  lines pop one?
- Why does swapping the two clauses of `reach/2` change whether the search
  ever answers, while swapping the two clauses of `ancestor/2` only changes
  the order of the answers?
- `Redo` resumes the goal's preserved execution state and executes the next untried clauses, searching for any potential matches and undoing variable bindings made previously, from whatever frame is currently at the top of the stack - which remained intact when it exited. A returned frame has already been popped from the stack, its memory was already deallocated and permanently lost and thus cannot resume from the last operation. It can be visually seen in the trace where we can see that `Redo` sits along the same level as the last `Exit`. 
