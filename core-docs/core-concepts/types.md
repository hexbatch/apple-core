# Types

Before creating an element, it has to have a design. Each type can have zero or more parents of other types.

The type contains the defined attributes of the element, the attributes can be static, live and or private.

Each type is owned by a user who can allow other users to create elements from it. 
The owner of the type can manage this via remotes called by the constructor action.

A type can do multiple inheritance, during the create and destroying of an element,
all the actions set up to listen to these events will be called.
