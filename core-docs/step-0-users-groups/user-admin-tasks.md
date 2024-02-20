# Admin api

Done via command (task to run on the command line)

## User operations

| Task             | todo | Operation                                           | Args                                                             |
|------------------|------|-----------------------------------------------------|------------------------------------------------------------------|
| create_user_auth |      | Makes/returns new token for a given user            | user guid or user element guid, or username. Optional expiration |
| logout_user      |      | Logs a given user out of all tokens                 | user guid or user element guid, or username                      |
| delete_user      | *    | Deletes a user if no elements in anyone else's sets | user guid or user element guid, or username                      |
| flag             | *    | flags a user                                        | see below                                                        |
| unflag           | *    | unflags a user                                      | see below                                                        |
| list_flags       | *    | shows who has what flag                             | can filter by flag type                                          |


# todo 
* delete_user : check for elements and types in other sets
* flag, unflag, list_flags : implement




# flagging users
adds|removes a system flag to mark users for system stuff:
All flags can be constrained by an end time, or even a schedule, so can moderate something for a day 

When a flag gives ability to see or change data, this means by only through direct api calls (get and set element attributes or core.users.read)
A flag can be updated with it has a path by adding the flag again, no need to remove

When a flag is removed its just deleted

Admin flags
* remote_types: allow them to add sensitive remotes like command and socket remotes
* remote_activity: allow them to see all remote activity, or filtered by a path (remote activity for just a type, or attibute family)
* user_read: allows to see all a user's attributes inheriting from a path (so can filter which types of users or even user meta)
* server_approval: allows to approve or ban a server manually
* moderate_read: optionally includes the family of types or attributes this is for with a path. Read otherwise hidden data
* moderate_write: optionally includes the family of types or attributes this is for with a path. Write to data that can be seen and in this path.
* remove_admin_flag: type of flag, or all
* do_user_flags: able to assign bans and unbans except to users with admin flags
* do_admin_flags: able to assign or remove non-user flags

User flags
* ban: bans a user until a future time, or forever, user is logged out, and nobody can make a new token for it
* unban - removes a ban

Because user types cannot be changed after an element is made from it, these flags are stored elsewhere

this stores both admin and non admin flags

    user_flag_table:
        user_id (who is this for)
        set_by_user_id (who did this)
        enum of flag
        path_id (optional for some flags)
        effective_until: (optional datetime this is valid for)
        schedule_id: (optional schedule this is enforcable at)
        created_at
        updated_at
