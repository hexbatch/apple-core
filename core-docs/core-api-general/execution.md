# Executing Api operations that write to tokens or make resources

The execution of each api should allow pauses and resumes based on stuff to wait on.
When an api executes, it will get a copy of what it is operating on, and after that not look at more recent changes to those.
When it finishes, it will write the changes to the attributes for others to see, and release any created resources so its seen outside of the api call

## Api Scope
Changes made during an api call is only seen inside that api call until its done
Option to throw away all changes if cannot write all changes. Cannot write to attributes that have been changed since the api call started

## Pauses:
Remotes can be designed to interrupt the execution of call, and then the core api allows a user to provide the waiting results and can get the data being sent to the remote.
It's like a human interacted remote.
When a call pauses, it serializes the copied values and what its doing, and when resumes deserializes itself.
So a pause can take any length of time

Core has no memory of completed api calls, only current waiting ones.


## Api for any call waiting
list waiting api made by the user
get details for a waiting call, or first waiting call so not needing to list
includes call to remotes:  details with data, and key value pairs needing to be filled out
update waiting to give task data
User who made the waiting can delete it if they want

For remotes without a uri, then the user must enter the data to be returned by the remote. There can be more than one remote needing manual updating


## When an api is called:

it gets a list of tokens to read, and then it goes into a bubble
if it has to wait to read a token, it is paused after getting a list of all waiting reads
a token can be waiting to read because of a remote of type pause, or an extra long time remote, or other issue
once it has all reads needed, then it either continues or unpauses
it only reads the data it cached, and does not do updates on what it reads for rest of api call
Events
gets a list of all events, calls them, and then maybe pauses again if cannot complete some
events cannot loop, if a value event or other loops back to trigger the same event again, that is stopped without causing an error
writes
event value changes are also writes, so has list of changes from above
api writes are added to that list
checks to see can write to all, if not pause
moves tokens via sets
if a token is needing to change sets, does it now (events already called for approval in above ) . No pause
creates new resources
no pause
created resources not available for use in the above
any events for permissions already called in step above
writes to the system
if api call option to fail all api if any cannot be written (because there is an update made since the api call started) then all above discarded
if api call option to allow fails, then write what we can
new resource creation can fail if name already taken, we do not know of name clashes until this phase, name clashes will remove the created here

writing an attribute will time stamp it

after an api call is finished, and outputs it response, there is no record. Only record of api calls is those paused


Pausing will serialize, in json, the state of the api (the data provided by in the api call, the user of the call, the read data, the events and writes, the waiting values needed)
once the writes stage is done it is not pausable anymore
the api calls to list and show details will get this serialized info
updating a waiting value or remote call will update the serialized until all needs met
when all needs met then is unpaused again