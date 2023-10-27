# System defined items

names of system defined items do not have the user in front of it and have no dots.
They do have aliases though.

There is an api to list the system items by type and role: for example list all the system attribute names, and those for identification

## Standard token types

### User Tokens

The user token has all the core identification and display attributes. When a user is created, a new token type is inherited

The base user token also is in some system defined groups

### Group Tokens

The group token has all the core identification and display attributes. When a group is created, a new token type is inherited

## Standard groups

* script_permission group : members here can create scripts

## Standard attributes

* Core ID and display
* Management flags
* Organization
* Copy
* Language

### Core identification and display

* name: string
* email: string
* phone: string
* address: string
* location: map_coordinates
* description: markdown
* image: binary
* symbol: binary (small image svg)
* primary_color: color
* background_color: color
* svg_symbol_image  : binary (small image svg)
* favicon : binary (regular image types) 32px square
* small_thumbnail: binary (regular image types) 128px square
* medium_thumbnail: binary (regular image types) 256px square

### Management flags

* allows_set: evaluated for truthful determines if a token can be added to a token set
* allows_set_operation : evaluated for truthful to see if the set operation can take place
* attribute_filter : if present, only the attribute named here in the target-attribute will be allowed, if the value is truthful

### Organization

Read only tags, to sort tokens. By default, tags can be read by everyone and written to by no one

Base tag attribute, which has direct children being tag categories, then more specific tags inherit from the categories.

Tags should be about what the token contains, or what the token is about

* user - the token is about a user
* media - the token has media such as image, pdf, or video urls
* documentation - the token has markdown files to explain stuff

### Copy flags

* origin_server_url string
* origin_token_guid string



