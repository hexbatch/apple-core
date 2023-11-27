# User services

* will get user details (with attribute values)
* will edit user details (edit attributes)
* will store and give a basic user token (to get standard attributes)
* stores and gives back user layer-only data
* creates, stores and gets the user_wallet, landing, and home set

# Api

## create user
    user_services.create_user
* calls job:create_user 
* stores the user data (bearer token, sets)
* calls `session.create`
* stores the first session id
* returns user data

## get user fields
    user_services.list_user_fields
* if cached data in good time range, return cached data
* calls `job:get_user_fields`
* stores the fields
* returns the fields

## get basic user token
    user_services.get_basic_user_auth
* returns stored auth


## stores user data
    user_services.store_layer_data
user data for layers only, not core

## gets user data
    user_services.read_layer_data
gets user data stored in the above

## read core user data
    user_services.read_core_data
* calls job:read_user
* returns the user data



# Jobs

--------------------------------------------

## job:create_user
Makes a new user. Fills in the user attributes on the user token. Makes the  user_wallet, landing, and home sets

Input data:
* user info

Pre layer calls:
* calls `permissions_layer.default_rate_setting` to get info to pass to core to create the new rates

Core calls:
* list of core calls 

Return data:
* user_wallet, landing, and home set ids
* bearer token
* rate set

-------------------------------------------

## job:get_user_fields
gets the standard description attribute names and descriptions

Input data:
* none

Core calls:
* core.standard.family.list

Return data:
* array of name, primitive type, ranges, and descriptions for each description

---------------------------------------------

## job:read_user
gets the standard description attribute names and descriptions

Input data:
* core user id that is wanting the data

Core calls:
* core.user.read

Return data:
* array of name, value for each description

---------------------------------------------