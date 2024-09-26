# Element Set

A set does not have any definition or structure, it's a loose organization of elements. A set must have an element defining it.
AN element can belong to one or more sets at the same time. Elements can be shared between sets.

AN element set is owned by the owner of the element that defines it.
But others' elements can be added to the set, if possible.



The defining element of a set can have its ownership transferred. This is also known as the set element.
Set elements are seen as normal elements unless in a set which has them as a child or link or parent.
Any element can make a set and still be a regular element.
Set elements can have action handlers for set events. An action handler processing the element-adding-to-set event can filter out elements using any logic

The element defining the set determines who can read (see the elements in it) and write to the set (do set operations on it).
This is by who can read and write to the element.

The defining element can have a location, and bounds, given to it, like any normal element.
This location can be used by set operations.



Elements about to be added, or it a set, have allergies and affinities. This can prevent the element from being added,
or it can cause the element to move to a relative of the set soon after its added.

Elements about to be added or removed can have their actions handle those events, and decline. Then the element is not moved.
Likewise, the element defining the set can have actions handle the event for the element entering and leaving the set.

A set can have a requirement to specify what elements are allowed in there.
If a set has a location bounds, then it has an option to only accept elements inside it that have no location set.
the option for location_checks can be turned on or off at set definition time


## Set relationships
[relationships](relationship-overview.md)
Element sets might be organized to have parents,siblings and links. There should be ways to navigate through this with the api.

## Group sets
[group sets](group-set-overview.md) allow groups to be used more in the api for many things


## Requirements
[sets.requirements.md](requirements-overview.md)
Requirements  specify what types are wanted, and amount of each of types.
I can make a requirement of a couple of types, and say the first type should be 5 to 8 elements, and the second type must be at least 10 in amount

Requirements are used in element set operations and anywhere there are some requirements to the types and amounts of elements.


## Set Operations
[sets.operations](operations-overview.md)
We can do operations on sets to make new sets, combine sets, and see what is in a set

## Definition

    So an element-set:
        id: the id of the set
        element: Every set has an element to define it, which adds ways to describe the set, search for it in path operations, or give it some location and time
        elements: []
        parent-element-set: (optional) may have a parent, used for organizing element sets. (cannot be cyclic)
        parent-context-set: may have a context parent in a context relationship (not related to the parent-element-set)
        linked-sets: (optional) may have links to other sets (can be cyclic so two sets can link to each other)
        requirement: id (optional), if there are max and min requirements, or not, this types the set and filters elements
        location_checks: true or false

# Requirements in a set definition

When a set has a requirement in its definition, the means only the types and quantity of elements are allowed into the set.
It can be that the requirement has a minimum of greater than 0 for one or more types.
This means that elements can only be added via set operations that have that many at the same time

for more fine-tuning, the set-element has the events run at it when an element is added or removed 

# Allergies and Affinities

AN elements total affinity and allergy is the sum of its attributes.

If there is no attraction to a set, and a repulsion, then the element cannot be added to the set.

However, if there is a mix or only attraction, then element can be added to the set.

If an element, already in a set, has more of an allergy to it, then it is not removed from the set automatically

## Allergies

Sometimes an attribute does not want to be in a set if another attribute is already in the set. this is set in the attributes allergy array

## Affinities

Sometimes an attribute must have another attribute to already exist in a set before it can join it. This is set in the attribute's affinity array

# Read and write permissions can be defined by set membership

attributes have the option to be readable or/and writable based on other attributes being present in the same set (not necessarily in the same element)

Between the ability to control when an element is added to a set, and when something is readable. This makes for a powerful set of access choices.

Additionally, user permission is by group, and group membership can be restricted to a boundary (only active in time or location)


# Set visibility
For an element to be inside a set, it needs to be able to see the set. A set can be in the global space of a server, seen by all in the server. 
Or it can be inside some other set, seen only by elements in that set or relations. 
A set in a parent set can be seen in the children sets. 
A linked set can have its sets seen by elements inside the linker. 
An element in a parent cannot see sets in children.
A linked set cannot see sets in its linker, unless it makes a link itself.
An api operation can try to put any element it can into a set. The element can go inside if:
* the user can read at least one attribute of the element
* the set is visible to the element

# Popping child sets

Sets can be created and destroyed by rules 

When an element is put into a child set, while, also in the parent set, 
and when that child set is destroyed (popped), the elements merge attribute values based on the new popped_writing_method .

Child sets cannot be popped if they have children.

If an element has a set B created by a rule, while that element is in a set A, then B is a child of A 
