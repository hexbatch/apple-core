# Executing Api operations that write to elements, do set operations, or make resources

An api operation will do something, and sometimes that calls a remote, or many remotes
A remote can be a url call, a pipe, a command, or other

This system is designed for long pauses and wait times for remotes to answer. 
There can be many different sources with different speeds.

Code is also designed to not allow things inside the system to initiate api calls themselves, the code only reacts to outside api calls.
This makes things simpler by a couple orders of magnitude.

One api call can start up several remotes, and the reponses from these can be combined (logic tree of remotes).
When a remote is called there can be a pause from a few microseconds to days or more. The wait is always unknown.
There is a timeout though, given, to any api that could call a remote, which means a timeout is an optional param when calling.
The default is set to some value. When a timeout happens, the api call fails, and nothing is done to alter the system.
A remote can register a status uri that is called with updates. If cancelling, then the remote can get that event and undo work made for the api call.

An api call can have many remotes that are combined logically and have their data combined too, 
or replaced by higher priority remotes (even if the lower priority returns before or after the higher priority) 
The remotes are organized and called in logical groups, and callbacks are sent to the code when they complete individually. 
When all the events of a tree are resolved, then the final response is created from all the responses,
and this determines the api opration and its values.

If, after all the remotes come back, that the api call is now impossible, that api call will fail.

Obviously, this makes for some very interesting timing problems.
But the internal data will be consistant, at any time.




## Api Scope

When an api call is made, any needed information is copied over to that call, so this means it is not depending on a stationary environment later.
It also means that the conditions can change while the api calls are being resolved and this is only noticed after all the remotes are done.

## Remote event callbacks

A remote can register additional uri which is used to send notification of success or failure to the remote.
This is useful when an api call fails and resources have to be changed on the remote.
The remote can track this because each remote call has a uuid.


## Can see api status 
There is an api to List waiting and complete api made by the user.
For remotes that require the user to send that data, there is a way to list and use that too.
