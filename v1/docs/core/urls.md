# Urls called to get attribute values

Urls can be assigned to attributes, to be called when getting an attribute value
There can be a time range this data is valid, so if the attribute is read again during this time, the url is not called again to get the value

Similar to scripts, the urls have a global and a local storage. If the url returns data, the local or global will be altered

* local state (stored in the token its attribute parent is attached to)
* global state (stored in the token type attribute that is made when an attribute having the url is attached to the token type)

when a url attribute is written to, the last valid timestamp is thrown out for the token (but not the token type!) and the write value is sent to the url

url is posted to : and params:
* global_state, local_state, write_value

url returns (optionally)
* changed keys in the global state (missing means no changes)
* changed keys in the local_state (missing means no changes)
* data good for local until timestamp (missing means no change to that timestamp for local)
* data good for global until timestamp (missing means no change to that timestamp for global)

if no timestamp, ever for local or global, the url will be called each time its read to

a url is always called on when written

the url callee keeps track of any state (state not stored here)

if there is some sort of login needed, the supported auth types are basic and bearer token, and there are fields set up for each

if additional post data is needing to be attached, that is provided. It is never updated except in the api

    url:
    user: required
    name : unique in urls
    uri: ip or url to call, also has optional different stuff like protocal, port, login stuff
    additional_post_data : constant json
    auth:
        auth_type:
        token:
        user:
        pw:
    returns primative or object


# Not just for http calls outside the cluster

can call private network ips or pipes etc