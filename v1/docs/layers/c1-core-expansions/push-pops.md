# Pushing and popping set operations

Add push and pop and queue and dequeue to set operations: tokens or set relationships can be done this way.
Events can decide to not do this.

When a token is applied, and its pushed or queued,
it's added to the set, and its given an ordering attribute, the order depends on the other order values of the other tokens, and what the operation is doing.
highest ordering for push, and lowest ordering for queue
The ordering can get negative, the default is 0 in a set that has no ordering.
tokens that are queued can be popped, and similar for the other way

When a token is applied, and its popped or dequeued then the token with the appropriate ordering is removed from the set,
highest ordering for pop, and lowest ordering for queue

When a set relationship is pushed or queued, the set is made into a child of the set holding it (so its token is still put in the set, but its in a child relationship state)
This allows ordering of children.

When a set relationship is dequeued or popped, then similar

instead of children, can do this with links



