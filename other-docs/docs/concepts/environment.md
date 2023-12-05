# There is a set each user interacts through

It's like interacting with a shell when logging into a linux. But multiple shells, in relationships

For instance, when I log into the layers I have my home set. This is all my saved stuff.

There is the concept of a "Working Set" that is the current set context the user does the api through. The working set can be changed.
The person queries the user layer to change the working set. 

The user's token is added to the set to be in, that way, the set can reject the user, or give a new token to the user (message, access, etc.).

A user can make an api call using a set for context that is not in his working set, it still works the same but the user's next api call will be his working set unless he changes it

A user can bookmark sets to travel to, and call the api to move his working set to that bookmark, or use that bookmark in an api call

A url resource found in a set can even be used to do some basic commands (similar to a program that is installed in a computer directory)

## Sessions

A user token can be in more than one set at a time. Each of these creates a session. Each user can only have one session per set.
When a session changes sets, the user api will remember the session data created in the previous set, and will restore it, if in the same session, when the user comes back to the set

A command pallet is given to the user for each set visited. This can be very basic, or be complex and changing for each command run

* the working set
* a command pallet
* session data

## Commands in sets

There can be a token with a known attribute, and reading or writing that token will do something (run a command via action).
If I go into a set and look for a token with a name to run things, such as say.hello, then there can be many different tokens with that name,
and in each shell these tokens can be similar or different. There should be a token of type command, that other tokens like this can inherit from.

But it provides a constant user experience to provide some standard tokens each shell.

### Command pallet

A user can be given a set of commands that can be used, this set of commands can be updated by something in the set. 
This can be a UI for the set. The user api supports a working set command pallet.

When the user executes a command that is on a command pallet, the set, or a token in the set, can update the user's command pallet to a new set of commands.

### Inheritance of commands via set relationship

It can be a waste of resources to make new command tokens for each shell, 
and if the command token is not there, keep going up the parent list until one is found, then use that

## types of sets for users

* Home set
* Wallet set (child of home)
* Message sets (mail, web stuff, child of home)
* Resource set (a set representing a computer or something in the world, there are agents there and scripts and uri etc )
* Community and regional sets
* store set
* organization set

## Set navigation

Often, one will want to go to a set with some attributes known, but not the set id. So a set token search will find the id, and the user joins the set

## Organization and store sets

When a user searches a map for things to buy, that map and icons and search is in a set run by an organization (created to do the map) and when they click on a token the user is in the store's set.

Each board or chat here has its own set for the participants to read and write messages. Some boards may have a set for each topic

## Landing set to visit a user's resources

A user can create their landing set, that people can join to interact with the user's stuff, without having to be in the user's group


## Set sessions

A user's preferences for the set, or even authentication where the user has to provide a sign on, can be stored in the set, and the data given an expiration date.
When the user leaves the set, this set associated data will be stored via the api user layer, and when the user, in the same session, comes back to the set, any non expired data in the session will be
put back into his session

## User drift

A user's token can be set to drift to explore new sets, and set a timer to change the set, if the change is going to happen, to the next one.
Or a user can create a token to drift like this, and it's progress can be followed by reading its set after it changes.
A token can be created that makes a new format html to send to the user when it changes, highlighting the attributes or tokens the user is interested in