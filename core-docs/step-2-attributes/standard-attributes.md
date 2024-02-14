# System defined items

names of system defined items do not have the user in front of it and have no dots.
They do have aliases though. These aliases are in the meta names under the lang codes.

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


### Types (base attribute standard_type)
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

* name: STRING.INFO.NAME
* email: EMAIL.INFO.EMAIL_ADDRESS
* phone: PHONE.INFO.PHONE_NUMBER
* address: STRING.INFO.ADDRESS
* location: MAP_LOCATION.INFO.LOCATION
* timezone: TIMEZONE.INFO.USE_TIMEZONE
* description: MARKDOWN.INFO.DESCRIPTION


## display (base attribute DISPLAY )
* primary_color:                                          color.display.primary_color
* secondary_color:                                        color.display.secondary_color
* background_color:                                       color.display.bg_color
* opacity - how transparent is this when drawn            number natural_number.display.opacity
* symbol: binary (small image svg)                        svg.display.symbol
* svg_symbol_image  :                                     svg.display.svg
* image-url (string for the url)                          url.display.image
* small_thumbnail: url                                    url.display.image.small_thumbnail              
* medium_thumbnail: url                                   url.display.image.medium_thumbnail
  


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





