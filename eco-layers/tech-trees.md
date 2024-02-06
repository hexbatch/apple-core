# Tech trees

A tech tree makes a family of elements that are ordered, so that possessing an element is the only way to get the next type element in the tree.

These elements start with a type, and each element given after that is a child of the type, so that I have to have element A to get its child B, and have B to get its child C
Once I have an element, I can add write stuff to the attributes on it, and if the attributes are done correctly, that element is destroyed

A tech tree can branch out, based on the attributes set on the earlier element

How a tech tree works is that event listeners on those attributes to write to, call remotes that destroy the previous element and gives the same set a new element

Getting a new element can be also coordinated with goals, so that the set receiving it, or the user, gets elements in reward.

Tech trees have many uses, but can be used to power an ecosystem:

In one scenario: conversions make editables to be consumed to get the next element in the tech tree 
(the editables were the first element and simply reading an attribute will achieve the goal)
However it can be made so that a certain number of different editables have to be read. 

Regardless the set that has the reader is given the next element.

That next element has to have its attributes filled out correctly to get the next element.

## Multiple required attributes to advancement

Should there be more than one attribute to fill in, the user to fill in the last remaining attribute gets the tech element.
If this is a tie, then one is chosen only, and the other does not get the element

All tech elements are destroyed when they generate a new element in the next level

