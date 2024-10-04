# Set relationships

Element sets might be organized to have parents,siblings and links. There should be ways to navigate through this with the api.
A relationship is defined by adding new elements to the sets which have attributes attuned to each other. 
    For parents and children, also the child set-definition-elements are inisde the parent set
These new elements are added or removed by the system when the relationships are created or destroyed


Note that there is not a restriction of the same user owning the parent and children. Also note that nested folders can be made.

This file structure of sets can be serialized and shared using the normal set serialization.

Children cannot be descendants to ancestors (no inheritance loops)

Links are one way and can be cyclic

Children are defined by the parent. Links are defined by the element doing the link to the other element

Links are stored in a specific type of attribute as the element id of the child or target

A set can make a link  by setting a new attribute dynamically on the set element whose value is the target set.
The attribute can also have an affinity for the target set, but the value is null. If the element of the set is in a set with the element that has the affinity,
Then dynamic linkage can happen. But if an allergy gets in the way, this link can be broken

Same sort of linking for child parent, but here, the attributes need to be on both parent and child and be reciprocal in their values (or affinities for dynamic)

Each link attribute can inherit from a link attribute base

Because links are exposed to the api as attributes, changing these attributes in actions or in set operations is allowed. This allows mass assigning and unassigning .


Set parents are in the child as an element, just as the child is in the parent as an element
* Removing either element from that set breaks the parent child relationship, and removes the parent child attributes
* Relationships for sets are still also defined by special defined attributes, and removing those also removes the elements from each other's sets, unless api calls says not to

When linking to a set, that element will be able to link if it can path the set, but the element is not part of that set


## parent child context

a set can have some or all of its elements added over to a new set. In a normal set operation, which adds or removes elements, this does not make that context.
But, if the create_context_set operation is made, then the new set made in that operation
    is a context child of the older set, where that element in the child can have a different value there.
When or if the child set is destroyed, then the data in the child and parent are merged

When a parent is destroyed, its children, leafs first, are destroyed in a way that the children are done first.
Elements are updated here when the set is destroyed, unless the operation prevents this

Its possible to destroy a child set without this data merge.

Parent children can do unlimited nesting, but a child can never be a parent to the parents above it.

