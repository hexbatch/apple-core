# Executing Api operations that write to elements, do set operations, or make resources

An api operation will do something, and sometimes that calls a remote, or many remotes.
When a remote is called there can be a pause from a few microseconds to days or more. The wait is always unknown.
There is a timeout though, given, to any api that could call a remote, which means a timeout is an optional param when calling.
The default is set to some value.

Each family of remotes that can be called has its own tree, and callbacks via event services are issued when the events complete.
When all the events of a tree are resolved, then the final response is created from all the responses, and this determines the api opration and its values.

Obviously, this makes for some very interesting timing problems, often and a lot! But elements can be moved from one set to another without conflict,
and the most recent decision will be the current action taken.
If, after all the remotes come back for something to happen that is now impossible, that api call will fail.

This system is designed for long pauses, and wait times.

It is also designed to not allow things inside the system to initiate actions, the code only reacts to outside api calls.
This makes things simpler by a couple orders of magnitude.

## Api Scope

When an api call is made, any needed information is copied over to that call, so this means it is not depending on a stationary environment later.




## Can see api status 
List waiting and complete api made by the user. For remotes that require the user to send that data, there is a way to list and use that too.
