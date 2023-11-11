# Layer permission service

* Add new layer api calls and default rules (useful when the layers grow)
* Add user exceptions (both extra and minus)

# API 

## can i do this
    permissions_layer.can_i_do_this

has a quick way to lookup to see if the layer api call is allowed by the rate set given.

The rate set might be a shared one, see deferred.