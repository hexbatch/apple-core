# User services

* remembers the user bearer token
* will get a new user bearer token
* will get user details (with attribute values)
* will edit user details (edit attributes)
* will store and give a basic user token (to get standard attributes)
* stores and gives back user layer-only data

# Api

## get basic user token
    user_services.get_basic_user_token
Will see if cached, if not then will create a new user, no frills, using the core api, cache that, and return the user token

## store user token
    user_services.store_bearer_token
Given a user id from the core, will store a bearer token

## stores user data
    user_services.store_user_data
user data for layers only, not core

## gets user data
    user_services.read_user_data
gets user data stored in the above