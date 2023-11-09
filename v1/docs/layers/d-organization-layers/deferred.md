# Deferred actions 

Make api calls in the layers using an agreement.

Make a script that can call http, but not allowed to file structure and is time limited. Can keep state the normal way.
This js script has a md5 hash, and this hash is part of the agreement.
Or can use a remote.

Users that are referenced to the script or remote input params can be variable or set to be specific. This is also part of the agreement.

Can use a token for a time bounds and time to run this after an agreement is reached. Can be run once, or a few times or periodically

This layer will run the script or remote at set times as long as agreement is truthful


The agreement will store the user to do the actions for, and whitelist of api calls to make and any constant params to the calls (allowing chosen params to be vars done at the user description)
the user to be proxied has to sign the agreement.

Any user participating in the agreement (that is agreed on and still in force) can do layer api calls while logged in as themselves.