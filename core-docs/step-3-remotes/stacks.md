# Stacks

Stacks are remotes acting in concert, waiting on other remotes to finish, which may take a long time.

A stack is a set with the stack element controlling it.
Each remote being run in a stack is a child set of the remote that is waiting on it to finish.
When the remote finishes it pops back into the parent, and some json operations are done to merge the waiting data.

Stacks can be seen as remote trees, where the leaf sets run first, and then report to their parents, and so on, until the original set is all updated,
Each child remote will update an attribute in the parent remote. The parent will either call to the outside or pass the failure up.
If there are multiple children, they each have their unique attribute in the parent remote to update, and then the bool logic will decide only after they all report.
The attribute rules will chain to do the logic. If the bool from the rule chain fails, it will not start the call but return failure to the parent to deal with.
False and truth are done by updating different attributes to activate different rule chains.

If a child remote fails, its parent may or may not run, depending on the boolean value given to it from the updated attribute

This can coordinate multiserver operations due to the callback type of remote, done by the other server. Which pauses the waiting stack.

Stacks can be interacted with as normal sets and elements.

Each remote in a stack can update the values of other element's attributes. 

The top set will write the final remote decisions that are joined together.

When a stack is not running, it is a collection of types, then the sets are made for the action.
And the elements or attributes to update are put into the top set.


# Actions are stacks

( need to update the action section)

# Events 
Events are attributes whose element is put into the stack, when there are nested events, 
such as the construction event for the creation of an element whose subtypes each have their event calling.
Then, the stack will be set up (defined in the type creation) to run this and the final answer will be a boolean .
The code will eventually get this bool, and if successful, allow the event to happen (creation, joining a set, etc).
The waiting things will be stored in a table, so when we finish this stack and the last attribute is updated , then it will pick that up 
in the next execution loop.
