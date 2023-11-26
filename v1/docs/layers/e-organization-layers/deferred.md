# Deferred actions 

The deferred is attached to the agreement during the creation of it and is part of the definition of the agreement.
Each agreement can have multiple deferred.

The deferred creates an agent which will call the api or a remote after an agreement succeeds.
And this can be run once, or a few times or periodically repeat, depending on the setup.

The api or remote has its call, params, and expected returns be md5 hashed to be included in the agreement.
