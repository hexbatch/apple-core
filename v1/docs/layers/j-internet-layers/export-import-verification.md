# Export, Import and Verification

Helps propagate and verify data between servers 

* Propagates token changes to registered urls.
    * sends changes out, filters can be applied to what changes to send for each url

* Listens to changes from other servers, and alters tokens on this server in response
    * can copy attributes to new tokens and basically clone stuff.

* Can verify that a token, or token set based on another server has certain properties or ranges of values in attributes, or regex in attributes.
* Verify that the serialized data received elsewhere is accurate
* Respond to verification requests

## Imported data has a way to be checked and mirrored

When importing data from another server, its sometimes necessary to verify the attributes before an operation.
The answer back contains a checksum that can be included in an api operation to that server, that api operation will fail if the checksum does not match for that resource (it was changed)