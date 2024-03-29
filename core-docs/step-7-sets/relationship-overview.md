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

When linking to a set, that set's element is in the linker's set, and follows the same rules as the parent child elements and special attributes

## Relationships as set contents

When a child or a link is added to the set, then the element of those sets are added to that set too.

Actions running on these sets can refuse being added to the set, even though their actions are ok with the event of creating that relationship.
Both sets of events have to be ok for the relationship to happen


Parents are given as set info when their element is listed, but the parent is also an attribute on the child.

When the relationship ends, the element of the set is taken out of the parent or linking set, but no events are called for this.

## parent child context

a set can have some or all of its elements added over to a new set. In a normal set operation, which adds or removes elements, this does not make that context.
But, if the create_context_set operation is made, then the new set made in that operation
    is a context child of the older set, and actions can write to the same elements in either set. So if there is an element A in one set, actions can only write to the element A,
but the element A in the parent or child can be written instead. They can have different values in their attributes after the context is created, and they are seperate values.

Otherwise, it's just like making a new set, except the children have to be destroyed before the parents are.
And the elements in the nested child that is destroyed have their changes thrown out, 
so the same elements in the parent set never have their values changed by operations in the child set, unless an action decides.
The same elements can be in unlimited nesting.
