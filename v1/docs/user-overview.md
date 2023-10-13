# User api

The user api is meant to be public facing and creates and alters users using the core api

The user logs in with oath2, and can grant access to other things if they want

Once the user logs in using the auth, the grants will be checked, and then the user api will use basic auth to the core

The user api will need to privately remember the password for the user to call the basic auth on its behalf

Because the user api controls all the public facing permissions, the other public api here are sharing the same authentication and check for the grants in the code

Other api can add their own grants

While internally, the user info is attributes

----------------------
## user api types of operations

* create user, edit user
* destroy user
* read user data
* list user groups
* create group, edit group
* change group membership or admins


## Authentication

The OAuth authorization flow uses authorizationUrl, tokenUrl and refreshUrl, these are specified in the open api doc

## Data structure

While the actual data is in attributes, the api here uses something more abstract, one does not need the guids for each system attribute to set

### User data

user data is either public or private, one needs a grant to read another's private data

Reading user data:

* name: string
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



if setting the images, a single image can be uploaded to generate the sizes, must be at least 256px square 
    (but can be rectangular and the starting point to crop can be added)

images can be file uploads or urls, optional starting crop point for medium thumbnail: below this is called an image
* url
* or binary file upload
* optional crop (x,y) start point

when editing, can provide just the fields to change, also can set different thumb or favicon by itself

new or edit user data:

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
* members: array of user data
* admins : array of user data
* token : guid of the group token if need more


writing group data is done by setting the name and/or description

Membership is done by the api calls in the group section 

## Operation list

* create user
* edit user
* delete user
* list groups
* create group
* add group member 
* remove group member
* edit group member

# Operations 

## Create User

create a new user

## Edit User

Edit user attributes

## Delete User

Removes identifying stuff from the user attributes. Any tokens owned by the user that are not in another wallet are deleted

## List groups

list the groups a user belongs to, as long as can see the attributes describing them

## Create a group

Based on a parent group(s)


## add group member

## remove group member

## edit group member

# Notes

https://swagger.io/docs/specification/authentication/oauth2/
