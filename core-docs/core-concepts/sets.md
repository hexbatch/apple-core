# Sets

Sets are collections of tokens, that are also represented by tokens themselves, and the set behavior is defined by that token and its attributes.

Sets can link to each other, have children and a parent. 

Users can put tokens they do not own into sets, as long as they can read some attribute on the token, then can add it to sets they control or can write to themselves.

Tokens can be designed to choose to not enter certain sets, or not leave them. Or only enter a set if there are certain attributes there in other tokens, or missing.
Tokens can limit themselves to being shared by a max number of sets at one time. Much more can be done with token interactions because they can be controlled by scripts and remote calls,
to decide what to do.

A token can be added to unlimited sets at the same time.

When a token is interacted with, its always in a set context.

Tokens sharing the same sets can change each other by:
* attributes change their readability and writability in the context of that set 
* changing attribute values or turning them on and off, or turning clusters of attributes on and off
  * this can be permanent for the token in all sets , until the next write; or just the current set
  * when the token is removed from the set, these changes are lost
  * but, in a parent set, child set, relationship, the changes in the parent are optionally remembered when the token comes back from the child.

Tokens can be searched for by the sets they are in 

There are also set operations, doing mass assign, and changes


