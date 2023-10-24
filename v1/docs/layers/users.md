# Users

This api handles:
* the reading of users
* the editing of existing users
* user groups : creating , editing, deleting groups
* user group admin stuff
* list user groups
* user wallet
* system functions for token use
* system functions for changing the public pw (the api for changing is done in the log in api layer)

The user layer here also remembers the user password, both the public one, and the one used to log into the core for the user.
It remembers the user token id, and stores the long term user bearer token

parts of this layer is public, and parts of this is for the system

this manages the home set, the first set context the user has when logged in and can easily find again


## Data structure

While the actual data is in attributes, the api here uses something more abstract, one does not need the guids for each system attribute to set

### User data

user data is either public or private, one needs a grant to read another users private data

Reading user data:

* name: string
* token : the user token
* guid : the user guid string
* description: markdown
* location (private)
* phone (private)
* email (private)
* address (private)
* schedule (time boundary applied to the user token)
* area (map boundary applied to the user token)
* symbol:
    * favicon_url:   (regular image types) 32px square
    * small_thumbnail_url:  (regular image types) 128px square
    * medium_thumbnail_url:  (regular image types) 256px square
    * original_image_url:   (regular image types)
* primary_color: color
* background_color: color
* landing set



if setting the images, a single image can be uploaded to generate the sizes, must be at least 256px square
(but can be rectangular and the starting point to crop can be added)

images can be file uploads or urls, optional starting crop point for medium thumbnail: below this is called an image
* url
* or binary file upload
* optional crop (x,y) start point

when editing, can provide just the fields to change, also can set different thumb or favicon by itself

edit user data:

* name: string
* description: markdown
* location : coordinate
* phone : string
* email : string
* address : string
* schedule (same as when setting time boundary)
* area (same as when setting map boundary)
* symbol:
    * favicon_url:   image (optional, will make from original if missing)
    * small_thumbnail_url:  image (optional, will make from original if missing)
    * medium_thumbnail_url:  image (optional, will make from original if missing)
    * original_image_url:   image
* primary_color: color
* background_color: color




### Group data

Can read group data if a member, Can set group data if an admin

All users are admins of their own user group, and members of the regular_user group, and can be added to other groups as needed

Reading group data:
* name : string
* description : markdown
* schedule (same as when setting time boundary)
* area (same as when setting map boundary)
* members: array of user data
* admins : array of user data
* token : guid of the group token if need more


writing group data is done by setting the name and/or description



## Listing Groups

Any member of a groups can see the full list of the group members and admins

## Groups Operation list

* create group
* edit group attributes (any admin)
* view group (any member)
* add group member (any admin)
* create a membership offer (any admin)
* remove group member (any admin)
* add admin (only if group owner)
* remove admin (only if group owner)
* change group ownership (only if owner)

### Membership offers

Membership offers can be sold in the marketplace, and allow the holder to redeem this for group membership. it only works one time

Because this is a token, it can also be a token pool, and also have bounds and expiration, and permissions (only some users can use it)

## User wallet

all the tokens a user owns is in a wallet, this can be organized

* list contents
* organize contents

# User environment

creates and manages the home set. There is a remembered set that the api uses as the context for the user, when he makes future api calls in the layers

## Working set

The api allows the person to change the set
Changes the set context the user looks through.
A user travels through the sets by joining and leaving sets. The set context the api calls are made from are made using this stored working set.

The user's token is added to the set to use as a context, that way, the set can reject the user, or give a new token to the user (message, access, etc)

A user can do an api call using a different set from his working set without leaving his working set. 
Everything still works the same, but at the end of the api call, the user is still in his chosen working set

## Bookmarks

a series of tokens based on a bookmark, found in the user home set

Api gives the ability to set the working set to a bookmark here

## Landing set

A user can create their landing set, that people can join to interact with the user's stuff, without having to be in the user's group.
This landing set is easily discoverable inheriting the landing type parent. Also this is in the user data given back, if the landing set's permissions allow it to be read
