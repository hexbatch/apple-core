# Deferred actions 

Make api calls in the layers using an agreement.

Each deferred is set for one user,
This can whitelist specific api calls for that user, and times to call, and any constant params to the calls 
    (allowing chosen params to be vars done at the user description), and can call a remote or script.
    The user in the deferred must match a user in the agreement.

Can use time bounds and time to run this after an agreement is reached. Can be run once, or a few times or periodically.
Or this can be run later, manually, by or more of the users in the agreement. The users doing this are logged in as themselves


If this uses a script. Script can return array and counts of allowed calls. Script on token and Can keep state the normal way.
Either script or remote has its call, params, and expected returns be md5 hashed as this is part of the agreement

Each agreement can have multiple deferred actions


This layer will run the script or remote at set times as long as agreement is truthful

The agreement will store the deferred, and the entire deferred is part of the agreement and will not be changed without cancelling the agreement.
