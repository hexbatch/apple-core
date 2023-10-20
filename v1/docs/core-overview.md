# Apple Core

The core api is not meant to be exposed directly to the public, but still needs basic auth and bearer tokens to use when the services call on it

The core is meant to be stand-alone for testing and demonstration purposes though

# Parts of the core api

* We have some objects (tokens) that are made out of attributes.
* A token has an owner and starts with some standard attributes. 
* A token is always in at least one token-set.
* A token can be in many token sets.
* A token set can contain tokens not owned by the owner of the token set.
* Token sets are altered, created and destroyed via set commands using type-groups
* Actions listening in on different lifecycle stages of a token, and when a token joins a set, can run javascript to decide to allow this and do auto transfers of tokens

Attributes are defined by themselves, and attached to the token-type. The tokens are instances of the token-type

# User authentication

Some public and read only api calls do not need to have a logged-in user.
Otherwise, can use both basic auth to get a bearer token.

A user needs to have many different bearer tokens that are valid. Once the user gets his bearer token, he can use an api call to get another one.

A bearer token can be generated, to use with jobs, so the pw does not have to be sent with the job data. But the jobs should have just temporary tokens they delete when done.

So, need an api call to delete/unregister a bearer token given to it


# Token types

[Token types](core/token_types.md) make tokens, and can select them from a set. They contain the static attributes that come to life when a token is made


# Tokens

Tokens are made from token types, and have live values of attributes

the token api will get its live attribute values, some or many of the token attribute depend on the set it is in.

Tokens can have attributes dynamically added to them, even if they are not in the token type. Attributes of the same name added this way overwrite the type attribute.
The user who owns the token can add attributes, also the token type owner can add attributes.

Static values can be changed just for this token. The actions have their own local state for this token.

Tokens also have a location, and an owner.

Having a location allows map bounded attributes to work. Attributes that have location bounds in a token without location automatically do not work, and are off.

This also means that some tokens cannot be taken to some locations or usable at some times.

Only the token owner can change who owns his token next. A set of tokens can have ownership changed.

A token can be affected by some attributes set in the token type, or dynamically.
* lifetime : this sets the bounds that the token can exist in, for instance will be deleted after a certain time. 

    So a token:
        user: must be one user
        token-type: 
        location:
            the lat and lon (optional)
        live attributes: 


# Token set

All tokens belong to one or more token sets.

A token set does not have any definition or structure, it's a loose organization of tokens.

A token set must be owned by only one user. Ownership is not transferred, but the tokens in one set can be added to the tokens in another set

A token set has a location given by the user token.

This location can be used by set operations.

## Set relationships

Token sets might be organized to have parents,siblings and links. There should be ways to navigate through this with the api.
Note that there is not a restriction of the same user owning the parent and children. Also note that nested folders can be made.

This file structure of sets can be serialized and shared using the normal set serialization.

Children cannot be descendants to ancestors (no inheritance loops)

Links are one way and can be cyclic 

Children are defined by the parent. Links are defined by the token doing the link to the other token

Links are stored in a specific type of attribute as the token id of the child or target

## Definition

    So a token-set:
        user: must be one user
        name: unique (optional) used for pathing of set paths for set boundaries (todo boundary type of set paths to read and write or action)
        tokens: []
        token: (optional) if some description is needed for this token set, or for identifying it with a set path
        parent-token-set: (optional) may have a parent, used for organizing token sets. (cannot be cyclic)
        linked-sets: (optional) may have links to other sets (can be cyclic so two sets can link to each other)

Tokens here can be reused and shared between sets, and have other roles at the same time

## Type groups

Type groups are used in token set operations

A token-type can be added into a type-group:

Tokens types can belong to one or more type-groups.

A type-group can be used in token-set operations, where tokens are added or removed between sets

Type-group can have a token to denote who owns it, and any attributes , to give it a name and appearance, or notes, and to provide logic for set operations
* Attributes can have those inherited from the attribute_filter which can look at the set to filter and decide which will be allowed

Ownership is not used when type-groups are used in set operations

The token types can have a max and min amounts. In set operations the exact amount used will default to be either the min,then max if min not set, or all available if neither

    So: a type-group:
        token: (optional) if some description is needed for this type-group, or for identifying it with a set path, or putting bounds of when this can be used
        token-types: [ {
            type: token-type
            minimum_needed: optional
            maximum_needed: optional
        }]

## Set operations 

When putting a token into a token set, using an operation, the allows_set is evaluated if the owners are not the same, or if present.

When using a set in an operation, the token set can have an attribute allows_set_operation which has to be truthful to proceed
The value of this can be a script and set by bounds, the script can do a filter for the type of set operation or what is being used in the operation

set operations:

* T is the type-group and is always optional, if missing it means all are operated on
* A is the source set
* B is a second source set
* D is the destination set
* M is a token type
* G is a token type guid
* P is export data for a token set
* S is an optional bounds for the tokens in the sets. This can be used in any operations. The tokens must be in these bounds. "
* Path-specifier can be added to any operation



        combine/add: A source, B source (optional),  T pattern, D destination
        remove: A source, T pattern, D destination / removes tokens from a set puts it in another set
        create set: => new empty set
        delete set: removes a set, fails if any token here is not already in another set
        edit_attribute => attribute name, attribute value , A source, T pattern
        change_owner => new owner id, A source, T pattern
        copy => P source, G token type guid from source , M destination token type, D destination
        count => A source, path specifier  > number 

### Relation operations

Finds related tokens in sets. Tokens are related by having common ancestors and parents.

These operations can also filter by getting the related tokens that have attributes in common

* Z is an array of attributes the current user can read


        find related: A source, B source,  Z optional attributes , D destination

sets can have children and links. 


### Gathering operations

Operations similar to grep of find for the attribute values and their static content, in a file structure (treat links like siblings in a folder or more accurately here sibling sets)

operations to make simple key value objects for each set ( singular or with siblings (links) or children) with attribute names the keys and static values
each token can be a new object of (attribute:value) and these can optionally be left alone or condensed to a single layer of key values
if condensed, then the values for each attribute turn into an array for each set

searching can filter static values via regex, numeric_range, comparison (comparisons can be nested), or strict string match

    search: A source,  Z  attributes , T optional pattern, options to recurse levels, to filter, to condense => simple object

#### Using tags to gather - path specifier

Sometimes want to find stuff in set relations, where there is a token in one set, and another token in a set elsewhere, or a token path, 

this token path can be sort of like a url apples/bananas/pears

this will start the search for any sets that have the apples token, then for any sibling or children sets that have bananas, then for any s or c sets that have pears, then do the search

optionally, there can be gaps in between the sets that have the tags, so we may not find apples in the parent set, but in some descendant, then the bananas would be further in a grandchild, etc

both tags and attribute names can be searched for this way, and the search combined

so, in this notation # means a token name, and . means an attribute and :x means value of x, and > means no gaps

that means to search for >#apples>.bears:2/#witches.broomsticks:wooden

would be to start looking in the top set for tokens called apples,
then for any immediate children or siblings if there is a set with an attribute of bears that has a value of 2,
for any descendant or sibling chain find witches token that have wooden broomsticks 

A path specifier can be added to any set operation

Once can count the path specifier in a set, this is used for some actions

### Global Set

    All tokens are in a global set (G) so if needing to find any token at all use G for A 

### Copy 

Copy allow tokens to be shared across servers operated by different people.

It takes the publicly visible attributes, and creates new tokens owned by the calling user with its attributes set to the public ones.
And has an originating data attributes: origin_server_url, origin_token_guid

When a token is verified to have this data, the server that owns it is called, and it can send back an answer, or can send back updated data

Token sets can be exported to be in a json like structure, converted to an object here

### export data

Token sets can be serialized to have the data in the attributes as key value pairs, as seen by the logged-in user.

Token set relations can also be serialized with the token set, if chosen, with references to the sibling, parent and children sets to be used to get their data


## Permissions for a token to be added to a set

By default, a token can always be added to a set if the set is owned by the same person who is owning the token.

By default, a token cannot be added to a set if they are owned by different users.

However, other people can add a token to their sets if the attribute allows_set has a truthful value

if the allows_set is falsy value, even the token owner cannot add to the token set

allows_set, being an attribute, can use a javascript to do complex logic to decide this

### Allergies

Sometimes an attribute does not want to be in a set if another attribute is already in the set. this is set in the attributes allergy array

### Affinities

Sometimes an attribute must have another attribute to already exist in a set before it can join it. This is set in the attribute's affinity array

## Read and write permissions can be defined by set membership

attributes have the option to be readable or/and writable based on other attributes being present in the same set (not necessarily in the same token)

Between the ability to control when a token is added to a set, and when something is readable. This makes for a powerful set of access choices.

Additionally, user permission is by group, and group membership can be restricted to a boundary (only active in time or location)

------------------------------------

# Boundaries can be on the map or in time.

[bounds](core/bounds.md) are only applied to attributes.

Each bounds have a location and/or time and/or set path component, either is optional

If there is no bounds, the attribute is always on. Else, the attribute is only read, written, and applied inside the bounds


----------------------------------------
# User 

A [user](core/users.md) is both a person (or bot) in this library, and a token type. Any tokens a user creates will inherit from this token type.

A user when created has some default attributes, some of which can only be read by the user.

When a user is created, a user group for it is also created. Any other user added to the group can read the private data. 
Any other user promoted to admin in the user group can write to the user attributes.

User tokens cannot be bounded, and they cannot run actions

----------------------------------------
# User Groups

A [user group](core/user_groups.md)  is a collection of users. These groups are used for permission lists, and are the bedrock of the permission system in this library

Actions do not run on the token of the user group


----------------------------------------

# Attributes

[attributes](core/attributes.md) are the core of the api here.

Attributes can be made to interact with one another, to require each other to be read or used, to set permissions and conditions for anything that happens in this api

-------------------------------

# Scripts
[scripts](core/scripts.md) are Javascript can be set to run and generate a value when a token attribute is read

# Urls
[urls](core/urls.md) are remote callbacks to be run and generate a value when a token attribute is read

# Actions

[actions](core/actions.md) are attribute values that are javascript that runs.

The actions also handle rate limiting, contracts, and whether a set action can happen


----------------------------------------------------


# Data types

each data type has its own set of api operations

data types:

    action
    map bounds
    time bounds
    attributes
    token-type
    type-group
    token
    token-set
    user-group
    user

-------------------------------------------------------------

# System defined items

## Standard token types

### User Tokens

The user token has all the core identification and display attributes. When a user is created, a new token type is inherited

The base user token also is in some system defined groups

### Group Tokens

The group token has all the core identification and display attributes. When a group is created, a new token type is inherited

## Standard groups

* regular_user : this user is a vanilla ordinary user without special privileges 
* full_admin_user : this user can read, write any attribute, and can create tokens inheriting from any attribute, and assign ownership to anyone of any resource, and do user group changes
    

## Standard attributes 

 * Core ID and display
 * Management flags
 * Organization
 * Copy

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



