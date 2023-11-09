# Goals

A set can have a goal to reach, that is calculated by numeric comparison

Goals are a search, that has some aggregate operation done on the results, which produces a number.
The number may be lower or higher than the goal.

When the number shifts closer to the goal, a custom event, a goal event, is given to the registered set.
Likewise, when the number gets further from the goal, a similar custom event is sent to the set

The frequency of checking for the goal can be set when making the goal

And frequency of either goal event sent can change based on an elastic curve going away or to the goal.

Actions on the set will process the goal, and most likely call a script or remote to do something to get the goal closer.

Goals can be paused

Goals can be nested and grouped in operation to produce more complex goals. So events can be sent for both the smaller goals and the more complex goals.

Meeting goals can be attached to a transaction, so the goal achiever gets tokens
