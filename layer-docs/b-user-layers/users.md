# Users

This api handles:
* the reading of users
* the editing of existing users




## Data structure

While the actual data is in attributes, the api here uses something more abstract, one does not need the guids for each system attribute to set

### User data

user data is either public or private, one needs a grant to read another users private data

Reading user data:

* name: string
* element : the user element
* guid : the user guid string
* description: markdown
* location (private)
* phone (private)
* email (private)
* address (private)
* schedule (time boundary applied to the user element)
* area (map boundary applied to the user element)
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



# API

## show user
    user.show

gets the user asked for, the data only returns the attributes the asking user can see


## show me
    user.me

get the data for the logged-in user, same as user.show with the id set to the current

# edit me
    user.edit

The user or the person in the user's admin group can edit the user data






