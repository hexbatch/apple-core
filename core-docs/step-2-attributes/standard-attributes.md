# System defined items

System defined items, they have the user of system.


There is an api to list the system items by type and role: for example list all the system attribute names, and those for identification

These always have the same hard coded uuids 

# Standard element types (base type is standard_type)


## User Type (standard_type.user)

Each user type inherits from the same base standard user type which has all the core identification and display attributes.
When a user is created, a new type is made just for the user.

## Remote type  (standard_type.remote)
When a remote has an element type, then it inherits from this and the user type


## Group Set Type  (standard_type.group)

The group-set type has all the core identification and display attributes. When a group-set is created, a new type is made



# Standard attributes



* Types
* ID
* Display
* Event
* Set Role
* Admin Role


### validators 
URL (validate as urlish)
SVG (validate https://github.com/darylldoyle/svg-sanitizer)
MAP_LOCATION (always map coord)
SHAPE_LOCATION (always tripple coord)
JSON (always array or object in json)
NUMBER (always a number)
NATURAL_NUMBER (always a number >= 0)
STRING (anything)
BINARY (anything binary string)
EMAIL (always email like)
PHONE (always e164)
TIMEZONE (as a named timezone)
XML (validate as xml)
MARKDOWN (???)
AUDIO  base attribute type for sound file urls - json has url , start at offset, loop, total play time
VIDEO  base attribute type for video urls - json has url , start at offset,  total play time
COLOR (validate as css standard color format)

### identification (base attribute INFO )

* name: info.name
* email: info.email
* phone: info.phone_number
* address: info.address
* location: info.location
* timezone: timezone
* description:info.description


## display (base attribute DISPLAY )
* primary_color:                                          display.primary_color
* secondary_color:                                        display.secondary_color
* background_color:                                       display.bg_color
* opacity - how transparent is this when drawn            display.opacity
* symbol: binary (small image svg)                        display.symbol
* svg_symbol_image  :                                     display.svg
* image-url (string for the url)                          display.image
* small_thumbnail: url                                    display.image.small_thumbnail              
* medium_thumbnail: url                                   display.image.medium_thumbnail
  


## events (base attribute event)
* see list of events

## type categories (base attribute type_category)
in addition to having special types, they are also marked by a similar attribute
* user
* remote
* group_set

## Set Role (base attribute set_role)
* see set relations
* see mutuals

## User types can have attributes added or removed at any time (base attribute admin_role)
* see user admin tasks





