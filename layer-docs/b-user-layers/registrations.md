# Registrations

Does all the new user account creation

* Allows plugins to be setup for different kinds of registration
* allows people to create accounts in different ways by using plugins
* Stores way to verify login based on plugin



## Signup Plugins

Each type of sign up has its own plugin. It has different data requirements and flow.
There might be extra api calls required by the client and plugin to fill in stuff.

The first plugin for registration is only for testing, or use in the api, only requiring a username and a password.


Plugins set their own pw requirements, if they even use passwords

Plugins are managed by composer, but there is a config set in the .env that sets a registration plugin to only be used for certain ips.
The simple registration may be whitelisted, or turned off when not needed


# Api

## Init form data so can display it 
    registrations.form.init
* calls `user_services.list_user_fields`
Form data is used by all plugins, it is the information needed. A plugin decides which info is mandatory

Calls the standard.family.list for the description args to make the form data. Will cache this, can be called again any time to get more recent

## List plugins
    registrations.choices
Will return a list of plugins with urls to use for registration, as well as what sort of information may be needed


## Show form to register
    registrations.show_fields
the plugin handles this.
shows the fields required, and some description for each, to register.
Will give the url to call.
The plugin will decide what to show, and the fields may vary a lot



## Register the user 
    registrations.create
* calls `user_services.create_user`
* calls `user_services.store_layer_data`
When the user submits the registration vai the plugin provided url,
the plugin may do some extra steps and make the client or user do more.
Finally, the user will be created, and the layer info for the user, the login credentials, will be stored

## Start reset login
* for the logged-in user, will show a list of urls to use (at least one!) to reset the login

## Reset login credentials
    registrations.reset_credentials
* calls `user_services.read_layer_data`
* using the selected plugin, will let it show forms and callback urls to reset credentials
* calls `user_services.store_layer_data`

# Registration plugins

Are activated , loaded using composer plugin setup. Do all configuring via console

They store the user credentials in the user-services
