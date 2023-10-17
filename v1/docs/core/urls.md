# Urls called to get attribute values

Urls can be assigned to attributes, to be called when getting an attribute value
There can be a time range this data is valid, so if the attribute is read again during this time, the url is not called again to get the value

Similar to scripts, the urls have a global and a local storage. If the url returns data, the local or global will be altered

* local state (stored in the token its attribute parent is attached to)
* global state (stored in the token type attribute that is made when an attribute having the url is attached to the token type)