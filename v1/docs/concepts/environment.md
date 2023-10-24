# There is a set each user interacts through

Its like interacting with a shell when logging into a linux. But multiple shells, in relationships

For instance, when I log into the layers I have my home set. This is all my saved stuff.

There is the concept of a "Working Set" that is the current set context the user does the api through. The working set can be changed.
The person queries the user layer to change the working set. 

The user's token is added to the set to be in, that way, the set can reject the user, or give a new token to the user (message, access, etc).

A user can make an api call using a set for context that is not in his working set, it still works the same but the user's next api call will be his working set unless he changes it

A user can bookmark sets to travel to, and call the api to move his working set to that bookmark, or use that bookmark in an api call

A url resource found in a set can even be used to do some basic commands (similar to a program that is installed in a computer directory)


## Commands in sets

There can be a token with a known attribute, and reading or writing that token will do something (run a command via action).
If I go into a set and look for a token with a name to run things, such as say.hello, then there can be many different tokens with that name,
and in each shell these tokens can be similar or different. There should be a token of type command, that other tokens like this can inherit from.

But it provides a constant user experience to provide some standard tokens each shell.

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