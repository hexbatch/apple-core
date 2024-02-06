# Items

An item is both a message and how to share info.
The original item itself is a type, and has constant static attributes to store text, links, markup, etc. 
If replying to the item, then a new child type is created from the original item type.

Elements can be made from the types to share information and make sets to organize the info. The sets can be used in transactions.


These elements can have boundaries and extra media put in: They can have a schedule and location they are seen, and be like announcements.

Those who can reply to an item are limited to the allowed parents user group, and the admins of the user who created the item.
This is enforced by each reply being a child of the thing that is being replied to.
Items can reply to two or more parent items, otherwise unrelated, at the same time.

Item elements can be sorted into sets.

Some or all of the info in the item can be made public readable, or only readable via a membership in a user group.

Contracts can be made to allow other users to be able to read the info, and/or reply to an item.

The item type has custom event when something replies to it, and then that is propagated to another event replied-to-descendant.
This means being able to reply to an item can do things outside the instance via remotes on the actions.

* Items can be used for access to an outside url or streaming service
* Items can reflect discussion boards, postings and feeds
* Items can hold invitations to other items, and announcements and messages to be rendered into html or other, to be delivered into people's wallet
* Items can be sorted into sets for organization via flag attributes provided by this api

Because items can reflect conversations and discussions, these are used by the board api to listen to, and create new items, when there are responses.


## Protected message set

Items can also have organized elements of itself in a set whose element is from the same type. So the set and items in it are all elements of the same type.
There can be organization here with parent child sets nested, again of the same type. Live attributes are added here to enforce with scripts removing the parent child relationship.
The elements in this set, and also nested sets, cannot be put into other sets, they are only to be in one set forever, until deleted


## Locking and unlocking

Information in an item can be encrypted. Only the users in the membership group of an item will be given the keys to use it. 
The key will be added to their wallet sets, and viewing software can use that to show the content.

But this key can be encrypted also, in another item, and the user must be able to be read, or reply to, another item user. In order to use that key



### Blocking and reporting and spam

Items can be reported on, can be individually blocked, and the user making the items can have a spam score, this puts their deliveries into the spam folder in a wallet

## Mixing and matching 

Items can also be created to mingle, and be combined in replies.
Some items may be needed to read the rest of the message.
This allows puzzles and games, as well as sets up the mechanics for additional things.


## Localized communities

Items can be open to any user in a location or time
