# Iteration:

There can be a cursor made (a filter with an attribute that has value of number representing the current order)
Applying this cursor to a set gets tokens or children in order (can choose)
Can use this iterator as a filter in any set operation
Same iterator can be used on several different sets, and can be reset at any time. If not reset and the newer set has no position of that kind, then nothing returned


Ordering in general:
It can happen that some tokens have the same order.
Same order rank will cause the above operations to skip all but one randomly chosen

There is a set operation to reset order so that all have a different order, same order things before will be next to each other in the new ordering
There is set operation to remove all ordering
Set operations to create, reset iterators

Iterators can allow loops to happen, with each api call.

A type of iterator does not keep track of the current index via its attribute, but assigns a current attribute to the tokens. This makes the current sticky across many different iterators,
but need permissions to the tokens to do that, and any token that is not allowing this attribute will be skipped, so is a great way to iterate writable tokens.



Any api call can provide a token or attribute using an iterator from a set (current token), can filter attribute(s)  to use.