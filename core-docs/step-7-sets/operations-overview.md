# Set operations

Do things with sets, great for filtering, comparing collections, or mass altering union


When having an element join or leave a set, the actions of each element can run

When changing attributes, mass attribute change actions can run on each element


Set operations:

* T is the requirement and is always optional, if missing it means all are operated on
* G is a group of users, and is always optional, who must own the elements to be used in the operation
* S is an element representing bounds for the filter in the set operations. This can be used in any operations. The elements must be in these bounds.
  Can specify if using map, time or both (path not used). This is always optional
* A is the source set, or element
* D,E is the destination set




        combine/add: A source, B source (optional),  T pattern,  G group,D destination
        difference: A source, B source ,  T pattern,  G group, D destination
        remove: A source, T pattern,  G group, D destination / removes elements from a set puts it in another (optional) set
        edit_attribute => attribute name, attribute value , A source, T pattern , G group
        change_owner => new owner id, A source, T pattern ,  G group
        copy => A source, B source ,  T pattern,  G group, D destination
        results => search ,  T Pattern ,  G group, D destination
        reorder => A source, attribute , sort order, A source
        pop|unshift => A source, B source
        push|shift => A source, B source
        find_common_elements => A source, B source ,  T pattern,  G group, D destination 
        remove_common_elements => A source, B source ,  T pattern,  G group, D destination 
        create_context_set => A source, T pattern , creates new D destiation set
        mutuals => A source, B source (optional),  T pattern,  G group,D destination
        split => A source, T type,  D destination, E destination
        join => A source, T type,  A source

Common elements:
    get common elements from a group of sets, put them in a new set. Can do opposite too: remove common elements from groups

Mutuals:
  starting with an element or set of elements, and a target set, find the mutual sets shared with these elements.
    can omit the element(s) and just provide a set, and will find all the mutual sets to it

pop push use element pk order


## Common flags for operations

* human set operations can use the human filter, which when used will filter out any element or attribute used in a filter that is marked as not human

## Operations events

set operations can have an optional event here to decline the operation, if any one declines, then  the operation fails
* allow_operation event
* 
# Requirements
Requiremens are rules in attributes, to put a requirement in a set operation use a type, which has rules

# split and join
* can join live type on an element, or set of elements, new attributes from type added to that element.
  * If the target has attributes in common with the live (same or ancestors on the target), then these are covered up, and the new attribute used
* can split off a live type, previously added as live, the target element same except those attributes removed that were given to by the live
  * if this was covering up a descendent or same type from earlier, it is now exposed again 
