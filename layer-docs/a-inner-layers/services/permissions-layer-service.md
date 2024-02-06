# Layer permission service

* Add new layer api calls and default rules (useful when the layers grow)
* Add user exceptions (both extra and minus)

# API 

## can I do this
    permissions_layer.can_i_do_this

checks to see if the user has passed in an alternate rates, 

has a quick way to lookup (set up by the rates service) to see if the layer api call is allowed by the rate set given.

The rate set might be a shared one, see deferred.

## get default rate info
    permissions_layer.default_rate_setting
Calls the rate layer with some default setting for a user
