# Urls called to get attribute values

Urls and program calls can be assigned to attributes, to be called when getting an attribute value, or writing an attribute value.

Remotes are created by themselves, and can be tested without an attribute.

Remotes attached to an attribute are called when that attribute is read or written to, depending on policy in the remote

# Definition of a remote

    remote:
        user: required
        name : unique in remotes
        is_retired: default false // if true then cannot be added to element types
        is_on : if off then all read and writes will fail and the remote not called
        timeout_seconds: if an attempt is made to sent to the remote, this is how many seconds until the read or write of the attribute ends in failure
       uri:
            uri_type: (none,url,socket,console,manual)
            uri_method (post, get, patch.. etc)
            uri_port:
            uri_string 
                
        read_policy:
            allow: bool
            cache: bool, if true then each last call updates the cache, and if same cache param key values then cache is used
            cache_ttl_seconds: how old the cache is allowed to be
            cache_keys: array of string keys to use for the cache, empty means cache returned always
        write_policy:
            allow: bool,
        data:
            input_attribute_map: array<name of attribute, name of key this is sent under>
            output_map: array<name of server output key or xml path, name of key output object will have>
            remote_data : key value pairs with remote_data_type ('none','basic_auth','bearer_auth','data','header') and name, value and is_secret
        call_schedule:
            rate_limit_max_per_unit: x
            rate_limit_unit_in_seconds: x
        state
            local_state_init: the initial state for per attribute or action
            element_state_init: the initial shared state for any element that has this an attribute or action with this remote
            type_state_init: the initial shared state for all elements of the same type that has this remote in an attribute or action
            global_state: shared by all usages of this remote

## Read and Write policy
When this remote is attached to an attribute, the attribute value can be read and written to. This determines what happens, or if this is allowed.
If the read policy says no, then that attribute is now allowed for reading.
If the write policy says no, then that attribute is now allowed for writing.
Either read or a write will call the server, unless the read cache is activated.

When waiting for the remote, after its called, and before its completed, other read or writes cannot be done

## output maps
The output is the output map applied to the server response. 

When this server is called, the server data can be a http status, a primitive (string),xml, json, headers, or other. 
However, it is mapped to object keys.

If xml, this is converted to json.

Header key values can be put in the output map for those to be included.

If a single key is in the output map, and this is a primitive returned, or only a http code, and no headers are matched, then that key will have that primitive
Otherwise, if this is json returned the keys are mapped, any headers can be mapped.
If no common keys in the map, the output will be empty.

the special map of http_value will be assigned the http reponse code

* The guid of the element the remote is associated with is also sent with the data as element_guid
* The guid of the attribute the remote is associated with is also sent with the data as attribute_guid
* The guid of the type the remote is associated with is also sent with the data as type_guid
* The guid of the element user the remote is associated with is also sent with the data as owner_guid
* The guid of the api call user the remote is associated with is also sent with the data as caller_guid

## input maps
The input_attribute_map will read the attribute values of the ones listed here that are attached same element, missing ones are ok.
The data structure created is sent to the remote as the data

## state and cache

The state is combined from the local, element, type and global. The earlier overwriting the later if same keys (deep union).
The state is sent with reading or writing

The caches, and history are stored in the local state, these key is not sent to the server. 
Under this key is the output mapped with the values the remote returned data.
There is also a live-by timeout for each set of input params in the cache.

When the server responds, if there are any matching keys at the different levels, that match to the output keys, then those keys are updated, 
with top level keys replacing content of other top level keys

## auth
can use basic or bearer auth for url

## call schedule
the remote can be rate limited, for writes this means not writable if exceeds limits.
The call times and numbers, and errors, and http codes are stored in the global_state.

timeout_seconds: is how long the total remote operation can last, regardless if communication is initiated.
Waiting to connect is hard coded based on uri type

## turning off
if turned off, then this remote is not used at all, and all reads and writes of the attribute its attached to will fail.
Can be turned back on.
Admin (command line terminal) only can do this

# Manual entry 

Remotes can be type manual, by not having a uri, and that is all that needs to be changed to make it manual.
When a remote is manual, the api call will pause until the user enters the answer needed.
This is done via the api call method handling. See  [execution.md](../core-api-general/execution.md)

