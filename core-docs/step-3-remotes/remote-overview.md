# Urls called to get attribute values

Urls and program calls can be assigned to attributes, to be called when getting an attribute value, or writing an attribute value.

Remotes are created by themselves, and can be tested without an attribute.

Remotes attached to an attribute are called when that attribute is read or written to, depending on policy in the remote.

Remotes power actions, and are called when that action has an event

Remotes can only write or read from their holder (the action or attribute), they cannot write or read other actions or attributes

Remotes handle their own state, this is made easier when each remote call is given information about the action, attribute,element, type and set its in.

# Definition of a remote

    remote:
        user: required
        usage_group: (optional)
        remote_element: (optional) This element is from the type 
        remote_element_type: (optional) This remote type inherits from the standard remote type and the user type of the creator
        name : unique in remotes
        is_retired: default false // if true then cannot be added to element types
        is_on : if off then all read and writes will fail and the remote not called
        uri:
            uri_type: (none,url,socket,console,manual)
            uri_method (post, get, patch, put, delete)
            uri_port:
            uri_string 
            uri_to_remote_format
            uri_from_remote_format
        cache:
            is_caching: bool, if true then each last call updates the cache, and if same cache param key values then cache is used
            cache_ttl_seconds: how old the cache is allowed to be
            cache_keys: array of set of allowed keys to use for the cache comparisons, empty means each response resets the cache
        data:
            from_remote_map: array<rule to convert data from the remote to value in (attr or action)>
            to_remote_map: array<rule to convert either pre-set value, or data in (attr or action) to some part of a data format to the remote>
            is_sending_context_to_remote: bool (default false)
        call_schedule:
            rate_limit_max_per_unit: x
            rate_limit_unit_in_seconds: x
            max_concurrent_calls: default 1
        



## to remote maps

The data to be sent to the remote is collected using the to_remote_map rules, which takes json data from the holder 
and converts it to headers, or xml, json or plaint text the remote is expecting. 
Constant data can also be included in these rules, which does not depend on the current data in the remote holder.

Header key values can be put in the output map for those to be included.


if the is_sending_context_to_remote: bool is on (default off)
then the following is also sent to the remote:
* The guid of the type the remote is associated with is also sent with the data as type_guid
* The guid of the element the remote is associated with is also sent with the data as element_guid
* The guid of the attribute the remote is associated with is also sent with the data as attribute_guid
* The guid of the element user the remote is associated with is also sent with the data as owner_guid
* The guid of the api call user the remote is associated with is also sent with the data as caller_guid

## from remote maps

When this remote is called, the remote data can be a http status, a primitive (string),xml, json, headers, or mix.
However, it is mapped to object keys inside the holder. If xml, this is converted to json.

The output from the remote response is converted to json values in the holder using the from_remote_rules.

Missing data in the remote response is ok 


## cache

Caches are used when there is more remote calls than allowed, if cache not enabled, or empty,
then this remote activity will end up in error


The caches are stored via implemetation decision. They store and return data based on the cache keys.
The cache keys can only contain predefined keys for the attribute, action, element, type, user  guids that are involved in the call,
if one wants to partition the cache along these lines. Its optional to include one or many

The live-by timeout applies for each set of input params in the cache.

When the remote responds, then if caching is enabled, the cache for that remote will be set/replaced
with a string made up on the ref ids denoted in the cache keys


## auth
can use basic or bearer auth for url

## call schedule
the remote can be rate limited, which means no more than this amount will be queued to run at any one time

Waiting to connect is hard coded based on uri type

## turning off
if turned off, then this remote is not used at all, and all reads and writes of the attribute its attached to will fail.
Can be turned back on.
Admin (command line terminal) only can do this

# Manual entry 

Remotes can be type manual, by not having a uri, and that is all that needs to be changed to make it manual.
When a remote is manual, the api call will pause until the user enters the answer needed.
This is done via the api call method handling. See  [execution.md](../core-api-general/execution.md)

# Remote activity and logging

Remotes will be logged when used to call or even for cache. Logged may be pruned after a while.

# Notifications to remote

Remotes can get notifications for the failure or the success of the api they are used.
This can be a different uri for either

