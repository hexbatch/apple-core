# Deferred actions 

The deferred is attached to the agreement during the creation of it and is part of the definition of the agreement.
Each agreement can have multiple deferred.

The deferred creates an agent which will call the api or a remote after an agreement succeeds.
And this is done immediately after the agreement succeeds.


The api or remote has its call, params, and expected returns be md5 hashed to be included in the agreement.

if the deferred action fails, the agreement will be marked as failed.
The failure of the deferred is the http code status of the api or remote call. anything 400 or above is fail
