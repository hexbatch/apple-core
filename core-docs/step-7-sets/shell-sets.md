# Shell sets

A shell can be created with an operation on a set to select all or some of the elements in that set, and add them to a new set without removing any.
A shell's elements can include those from more than one set.
A shell is also a set, and so can be included as an element in any set.
Any set's defining token, the one that controls the set, can be inside a shell, or many shells, at the same time. See question below.

Elements in a shell context can still be in regular sets, but when an element is put into a new set, its not in a shell context.
Shells are not accessable to api set operations, or searches

Shells can be created from shells.

The changes to the elements here, if not to the static, will be only seen in this shell.

When selected to be in a shell, an element can be in three modes:
* when shell exits, the parent context (global or higher shell) will have that value copied over with the element value.
* when shell exits, the parent context (global or higher shell) will have that value merged with the element value.
* when shell exits, any changes will be ignored

individual elements can be removed from a shell, before it exits, but their value changes in the shell is lost.


# Questions

* what starts a shell (or calls the start shell operation?)
  * Can an entire set have some sort of value to be used in a decision to start a shell? 
    * Can the attributes in the set's defining elements have a defined value that can be evaluated?
  * An action can start it, by calling a remote that calls the api to do that. But is that the only way?
* how does a shell end
  * what happens if shell ends that has children or even descendants, do all the children, descendent shells get erased?
  * can an action just stop it, by calling a remote that calls the api to do that. But is that the only way?

# More
shells provide blocks of code(ish) and loop ability, resetting state at the end of the block or loop.
Can logic be defined by the overal state of a set? (see question above about set value).
Can a shell automatically start if a set has some overall value? Can a shell stop when that shell has an overal value?

By overall value, I mean a set condition of one, some or all the elements inside? Does a path have to be true for this logic to work?
Can I set up a path, and when that is truthful, then a shell will start, using all the elements in the set/shell that the path toggles to be a new shell?
And likewise, another path, if truthful, can end the shell?

Is this path setup on an action? How to avoid a cascading effect of too many shells?

----------

* when two or more sets are elements inside another set, can there be operations based on the overal set values?
  * These operations can produce shells or other sets?
  * Is set state changed inside a shell if it's an element in a shell?
  * are there more than logic operations? 
  * how to set up these logic rules, and what happens when it is truthful?
  * is it path logic that can be nested?
    * so if I set up different paths having groupings of boolean logic, how to apply the results?
    * obviously, this can be done in any remote. Is that the only way?

Some of its action listeners may depend on the values inside the shell context attributes of the set element.
The action listers of a set may have different behaviors based on if an element is being added or removed from a set based on the context.
* Is there any context for adding or removing set members? Or is only the global value of the attributes here used regardless?
* Can a set be created and destroyed or altered in a shell context? Or is this only global?
  * If it's in a context, is the shell element a member of that context?
  * Are there multiple versions of that set's membership? Context and global? or more likely a set contents never changes


# when asking if this is the only way for shell creation, destruction and using set path logic

Should this be not only done by remotes? Or is there more than actions listening reading to update these remotes which give the orders?
