# Urls called to get attribute values

Urls and program calls can be assigned to attributes, to be called when getting an attribute value, or writing an attribute value.
Urls can be set up to be called for either, or just one, with a frequency of how often calls are made, for each, to allow rate limiting.

## Reading and writing

There are rules that can be set up to how often, and what happens, when a remote is written to or read from.

Similar to scripts, the urls have a global and a local storage. But the remote does not use this, and does not see this.
The storage is for keeping track about how often its called, and if it should be called again:

* local state (stored in the token its attribute parent is attached to)
* global state (stored in the token type attribute that is made when an attribute having the url is attached to the token type)


As an attribute write value, remotes do not have to be called each and every time. This means writing to the attribute may be ignored or delayed.
If this happens the write will be treated as done, but the read will not work unless the remote allows caching

The read will only be possible when the server has answered back. Between the write and the server answering, the attribute holding this url will be unreadable by anyone.
If the owner queries it, the value will be marked as (pending) or something like that.

Multiple writes can be collected together at the token or type level. Then after a certain period, the server is called for each.
Each write value is paired with the token guid in the storage, so that when the server reports back, the state of each token is updated for the read.

So, for attribute reading and writing:
* If the remote is configured to be only called when writing:
  * If the last write happened before the read, over never written to, and the remote is not pending, then the value is read immediately
* if the remote is configured to be called when reading, then the server has to answer in N ms (not changable so not part of definition)
     or the read is considered invalid (attribute cannot be read)
  * This works if the remote is a nearby service on the same machine listening to a port, or something else fast 
  * There can be a read cool-down, so that if the attribute is read again during this time, the remote is not called again to get the value, but use the previous value
  * likewise the remote can be configured to not allow reads during this cool-down

There are also optional rate limits set to limit calls to so many per unit of time

## Data Going to the remote 

* The data a remote is sent can be packaged in other data, defined in the remote definition.
* The gui of the token the data is associated with is also sent with the data 
* current_attributes (names and values) of the token: {}
* current token owner
* current api user
* the earlier value of the attribute this is on
* extra_input_params can be tied to other attributes not on the token, by the action. If not bound, these are not sent

when gathering the current_attributes:
* Other remote attribute values are not sent unless there can be a cached read (so no remotes calling each other in endless cycles)

### Data coming from the url

Remotes can return a status, a primitive value (string or numeric), or json or xml.
if xml, this is converted to json.
The return is the value to read, but output keys can match up to top level json, and these output keys can be mapped to writing other attributes via the action

* changed keys in the global state (missing means no changes)
* changed keys in the local_state (missing means no changes)
* data good for local until timestamp (missing means no change to that timestamp for local)
* data good for global until timestamp (missing means no change to that timestamp for global)

### Other Settings

* If there is some sort of login needed, the supported auth types are basic and bearer token, and there are fields set up for each
* settings for how to call: IP, port, url, protocol, http method


# Definition of a remote

    remote:
        user: required
        name : unique in urls
        is_retired: default false // if true then cannot be added to token types
        is_on : if off then all read and writes will fail and the remote not called
        redirect: id of another remote
        uri: 
            url: (can be ip)
                method:
                port:
            socket: ( if set the url is ignored)
                port:
        auth:
            auth_type:
            token:
            user:
            pw:
        data:
            additional_post_data : constant json
            extra_input_params
            output_keys
        read_policy:
            allow: yes or no
            cool_down: (optional)
            allow_during_cool_down: yes or no
        write_policy:
            allow:
            cool_down: (optinal)
            allow_during_cool_down: yes or no
            cool_down_policy: cluster or use last write only
        call_schedule:
            max_calls_per_unit: x
            unit_in_seconds: x


# Not just for http calls outside the cluster

can call private network ips or pipes etc

# Permissions

* The users who can create a script are in the remote_permission group

# Manual entry 

Remotes can be type manual, by not having a uri, and that is all that needs to be changed to make it manual.
When a remote is manual, the api call will pause until the user enters the answer needed.
This is done via the api call method handling. See  [execution.md](../core-api-general/execution.md)
