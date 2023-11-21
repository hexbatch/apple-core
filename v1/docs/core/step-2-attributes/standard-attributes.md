# System defined items

names of system defined items do not have the user in front of it and have no dots.
They do have aliases though.

There is an api to list the system items by type and role: for example list all the system attribute names, and those for identification

# Standard token types

## User Tokens

The user token has all the core identification and display attributes. When a user is created, a new token type is inherited

The base user token also is in some system defined groups

## User Group Tokens

The group token has all the core identification and display attributes. When a group is created, a new token type is inherited

# Standard groups

* script_permission group : members here can create scripts

# Standard attributes


* Core ID and display
* Organization
* Copy
* Language
* Events

### Core identification and display

* name: string
* email: string
* phone: string
* address: string
* location: map_coordinates
* user_timezone: the timezone that can be default, if null then use system time zone
* description: markdown
* image: binary - base attribute
* symbol: binary (small image svg)
* primary_color: color
* secondary_color: color
* background_color: color
* svg_symbol_image  : binary (small image svg)
* favicon : binary (regular image types) 32px square
* small_thumbnail: binary (regular image types) 128px square
* medium_thumbnail: binary (regular image types) 256px square
* current_location_map: lat,lng
* current_location_cartesian: x,y,z
* shape_cartesian -- the shape is centered at the current location
* shape_map -- the shape is centered at the current location 
* transparency - number to use when the shape is being rendered by software for color transparency
* texture - binary (if renderer wants texture for a shape)
* model - binary (to store rendering models)
* audio - base attribute type for sound file urls - json has url , start at offset, loop, total play time
* video - base attribute type for video urls - json has url , start at offset,  total play time
* (for sets when token enters) default position inside set. When a token enters, if it does not have its positioning attribute set, then assigned this

### Organization

Read only tags, to sort tokens. By default, tags can be read by everyone and written to by no one

Base tag attribute, which has direct children being tag categories, then more specific tags inherit from the categories.

Tags should be about what the token contains, or what the token is about

* user - the token is about a user
* media - the token has media such as image, pdf, or video urls
* media-url -? the attribute has a url for viewing
* media-mime - the mime type of the media
* documentation - the token has markdown files to explain stuff
* file - this token is some uploaded thing, it can be media or not
* folder - this set acts like a folder to store files




## Events are attributes

Each event listed in the actions is an attribute that is assigned a truthful or false value. False attributes block the event from happening


# Role attributes

When a token is also a set, view, container, group, or represents a user, it has an attribute showing that. A filter can filter api types with this attribute set to that type





