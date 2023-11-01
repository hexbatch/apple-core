# Users

This api handles:
* the reading of users
* the editing of existing users
* user groups : creating , editing, deleting groups
* user group admin stuff
* list user groups
* api to sessions and their command pallets



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
* home set (private)
* session list  (private)



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
* remove group member (any admin)
* add admin (only if group owner)
* remove admin (only if group owner)
* change group ownership (only if owner)





# User environment

The api here sets up the environment for api calls that made for the user.



## Landing set and Home set and Wallet

### Landing 
A user can create their landing set, that people can join to interact with the user's stuff, without having to be in the user's group.
This landing set is easily discoverable inheriting the landing type parent. Also, this is in the user data given back, if the landing set's permissions allow it to be read.

### Home
Each user is also given a home set.
The default user session is from the home set, and the home set can store stuff not in the command pallet.

### User wallet

All the tokens a user owns, that is not some file or action, is in a wallet, this can be organized
We create the wallet when user registered.
The wallet can be organized like other tokens and sets


# Sessions 

## Concept of Working set

The api allows the person to create sessions and change the set
In a session, this changes the set context the user looks through.
A user travels through the sets by joining and leaving sets.
When a user session changes the set, the working set is changed. Here, the user is using the user api to navigate through the sets.
The set context the api calls are made from, in all the layers, are made using a session.
This means for most of the other api calls made in the layers, the user's working set is the context they use.
And all the other layer api needs to refer to this, which will be set in the user-services for easy access.

When a user session changes to a new set:
The user's token is added to the set to use as a context, that way, the set can reject the user, or give a new token to the user (message, access, etc)

A user can do an api call using a different set than his working set without leaving his working set.
Everything still works the same, but at the end of the api call, the user is still in his chosen working set


## Session list
A user can have different sessions at one time. A session can have three things:

* the working set
* a command pallet
* session data

The api here gives the ability to list and change sessions, and to do session stuff, such list the contents of a set, see his command pallet, and navigate sets

## Command pallet plugins

The command pallet is generated by action plugins, the user api here decides which plugins are used for which, or all, users

These commands are urls that can be called to do something

# API

## show session
    user.show_session

The logged-in user can select a session id, or none to use the default session.
Then the return will show the sets and tokens in the working set of the session, along with the command pallet urls

current_set:
  set_name: 
  set_author: (owner)
Contents:
   tokens: ( a page of tokens with urls to inspect) the child and linked sets are also tokens here, and the set status will show up in the info
            each token has some standard attributes listed (name, image or other appearance, description)
   next_url: ( a url to get this current set but with the next page of the token contents) 
Commands:
   a list of urls and descriptions and names of what can do
    there are navigation commands (go up, go back, home, etc), a create bookmark command url, a bookmark set url, and whatever else plugins add in



