# Actions

Actions are tokens seen in a set, and when the action command is run on them, in the session service, they do things. 
What they do is defined in this service

The actions service can be extended by plugins found in the users, which organizes actions for the user, and allow new actions to be created.

This service provides two actions: 

* create bookmark
* use bookmark

When the session changes sets, it can ask for a command pallet via an event filter,
This service listens to that, and will return the create-bookmark, and a set of all created bookmarks, to be seen by the user in the session only 
(so these are not really part of the set the user is in, but the command pallet seen in a different area of the data)


## Bookmarks

a series of tokens based on a bookmark idea. 
* The user can remember a set he visits, and make a shortcut to visit it later.
  * Each set can only have one bookmark.
* When the bookmark is acted on, Api gives the ability to set the working set to a bookmark here.

* A bookmark can be edited using a public grant later.
