# Shell sets

A shell can be created with an operation on a set to select all or some of the elements in that set, and add them to a new set without removing any.

Elements in a shell context can still be in regular sets, but when an element is put into a new set, its not in a shell context.

Shells can be created from shells.

The changes to the elements here, if not to the static, will be only seen in this shell.

When selected to be in a shell, an element can be in three modes:
* when shell exits, the parent context (global or higher shell) will have that value copied over with the element value.
* when shell exits, the parent context (global or higher shell) will have that value merged with the element value.
* when shell exits, any changes will be ignored

individual elements can be removed from a shell, before it exits, but their value changes in the shell is lost.
