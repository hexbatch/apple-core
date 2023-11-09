# Tech trees

A tech tree makes a family of tokens that are ordered, so that possessing a token is the only way to get the next type token in the tree.

These tokens start with a type, and each token given after that is a child of the type, so that I have to have token A to get its child B, and have B to get its child C
Once I have a token, I can add write stuff to the attributes on it, and if the attributes are done correctly, that token is destroyed

A tech tree can branch out, based on the attributes set on the earlier token

How a tech tree works is that event listeners on those attributes to write to, call remotes that destroy the previous token and gives the same set a new token

Getting a new token can be also coordinated with goals, so that the set receiving it, or the user, gets tokens in reward.

Tech trees have many uses, but can be used to power an ecosystem:

In one scenario: conversions make editables to be consumed to get the next token in the tech tree 
(the editables were the first token and simply reading an attribute will achieve the goal)
However it can be made so that a certain number of different editables have to be read. 

Regardless the set that has the reader is given the next token.

That next token has to have its attributes filled out correctly to get the next token

