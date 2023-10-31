# Registrations

Does all the new user account creation

* Allows plugins to be setup for different kinds of registration
* allows people to create accounts using different social media, using plugins
* Handles password reset if user lost it, based on plugin
* Stores way to verify login based on plugin
* Links each user created from here to one or more plugins with login credentials


## Signup Plugins

Each social network, or type of sign up such as email,
has its own plugin that gets the data, perhaps requires extra api calls by the client to fill in stuff.

Plan to do:
* the testing one for just entering username
* registration via email

## Linking Plugins

Each social network, or type of sign up, has a way to verify the ownership of the entry with the signed in user

Plan to do email verification first.


## Usage of agents

Agents api might be used for some, or all, verification and sign in, using a base user account 

(all users inherit from a base user token, which is system defined token but this can be a real user account too, so can grant access to the agent)


# Api

## Init form data so can display it 
    registrations.form.init

Form data is used by all plugins, its the information needed. A plugin decides which info is mandatory

Calls the standard.family.list for the description args to make the form data. Will cache this, can be called again any time to get more recent

## List plugins
    registrations.list_plugins
Will return the list in machine format.
But also will give a page a person can select from.

## Use plugin for session
    registrations.use_plugin
Will set the url to select a plugin 

## Show form to register
    registrations.show_form
The plugin selected will figure out the form and will either autofill it, and go directly to the registrations.create.
Or the plugin will prefill some or no data first, and show a form.
The plugin will show whatever pages or use callback urls to complete process


## Show secondary form to register
    registrations.add_registration
The plugin selected will figure out the form for the new registration and will either autofill it, and go directly to the registrations.link.
Or the plugin will prefill some or no data first, and show a form.
The plugin will show whatever pages or use callback urls to complete process

## Link registrations
    registrations.link_registration
The user will have the extra login credentials set to his account here

## Register the user when the form is submitted 
    registrations.create
When the user submits the first registration form, the creation will be put to a job

## Store login credentials
    registrations.store_credentials
using the selected plugin, will give/pass the credentials to it

## Reset login credentials
    registrations.reset_credentials
using the selected plugin, will let it show forms and callback urls to reset credentials


# Registration plugins

are activated , loaded using composer plugin setup. Do all configuring via console