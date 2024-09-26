# Actions



## Events 

see [events.md](events.md)

--------------------------------


# Action run order (priority)
Actions can be both filter and action change.

* Actions that respond to the same event can be given an optional priority order, and the actions are run from the lowest to the highest
* The highest priority action will approve or deny the event, if more than one have same priority, then any one can approve and the others ignored
* Many actions can do things to the same target, the highest priority will be the one used
* Voids are always run
* If more than one action is responding to the same event, this becomes a filter
  * the lowest priority will run first, and its value to set is passed to the next highest one, until all the actions have run. The highest priority action will have final say
  * the value can change data type, earlier actions can send up json with flags, and the final one can produce a primitive, or filter out json 
  * The passed value will be put into the remote params as the original value to change



## Filtering 

Some events allow data to be attached to them  
Lower priority actions are given the data returned by the higher priority actions, 
    and can also alter this data, or discard it, before sending their version of the data to the finish or next in the filtering list

# Constant data 

Actions can be defined with constant data
* Constants can optionally be applied to event data after server data is applied to it
* Constants can optionally be applied to data being recieved from remote before anything else is done.
* Constants can be optinionally applied to data being sent to a remote to go out, before that data is refined by the remote for sending.


#  action  hooks

A new stack can be set to run at any stage of an action
