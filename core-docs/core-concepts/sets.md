# Sets

Sets are collections of elements, that are also represented by elements themselves, and the set behavior is defined by that element and its attributes.

Sets can link to each other, have children and a parent. 

Users can put elements they do not own into sets, as long as they can read some attribute on the element, then can add it to sets they control or can write to themselves.

Elements can be designed to choose to not enter certain sets, or not leave them. Or only enter a set if there are certain attributes there in other elements, or missing.
Elements can limit themselves to being shared by a max number of sets at one time. Much more can be done with element interactions because they can be controlled by actions,
to decide what to do.

AN element can be added to unlimited sets at the same time.

When an element is interacted with, its always in a set context.

Elements sharing the same sets can change each other by:
* attributes change their readability and writability in the context of that set 
* changing attribute values or turning them on and off, or turning clusters of attributes on and off
  * this can be permanent for the element in all sets , until the next write; or just the current set
  * when the element is removed from the set, these changes are lost
  * but, in a parent set, child set, relationship, the changes in the parent are optionally remembered when the element comes back from the child.

Elements can be searched for by the sets they are in 

There are also set operations, doing mass assign, and changes


