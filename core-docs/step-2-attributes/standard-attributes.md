# System defined items

System defined items, they have the user of system.


There is an api to list the system items by type and role: for example list all the system attribute names, and those for identification

These always have the same hard coded uuids.

When a standard attribute is used, a new attribute is created that inherits from it



# Standard attributes

Base server attribute (it has its own gui) is used to make the base standard attribute, whose guid is defined

* Types
* ID
* Display
* Data
* Content
* Event
* Servers
* Set Role


### standard attribute validators 
URL (validate as urlish)
SVG (validate https://github.com/darylldoyle/svg-sanitizer)
MAP_LOCATION (always map coord)
SHAPE_LOCATION (always tripple coord)
NATURAL_NUMBER (always a number >= 0)
STRING (anything)
EMAIL (always email like)
PHONE (always e164)
TIMEZONE (as a named timezone)
COLOR (validate as css standard color format)

### identification (base attribute INFO )

* name: info.name
* email: info.email
* phone: info.phone_number
* address: info.address
* location: info.location
* timezone: timezone
* description:info.description
* preferred languages and weights
* iso region or locality

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
  

## data (base attribute DATA)
* starts_at  iso_8601
* ends_at iso_8601
* created_at iso_8601
* updated_at iso_8601
* domain includes subdomain, not path or protocol
* identifier any
* size_px number
* size_cm number
* weight_kg number

# Content (base attribute Content)
* author
* copywrite
* url
* rating
* mime_type
* keywords
* language_code
* iso_region

## events (base attribute event)
* see list of events

## servers
* domain name or subdomain
* reputation

## Set Role (base attribute set_role)
* see set relations
* see mutuals






