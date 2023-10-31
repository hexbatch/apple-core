# sessions

A user can have different sessions at one time. 

Each session has:
* an id
* the core user_id
* the layer user_id
* a name
* the working set
* a command pallet - a set that allows tokens to have well known attributes to read and write from
  * each token has a sorting attribute, a read attribute and a write attribute. These can be remotes or scripts 
* session data - a set that stores tokens used to remember stuff about this session


# API

# create session
    session.create
* Makes new db row 
* calls job:create_session
* fills db row in with the job output
* return session id

# destroy  session
    session.create
* calls job:destroy_session
* deletes db row when get success

# get session
    session.get
* returns session data

# list sessions
    sessions.list
* returns all the sessions for the user


# Jobs

## job:create_session

Creates what is needed for a user session to start

Input data:
* user id, auth token, name of session, id of session

Core calls:
* list of core calls

Return data:
* session data to store, includes the id passed in, and the name


## job:destroy_session
Destroys the resources from a user session

Input data:
* session data, auth token

Core calls:
* list of core calls

Return data:
* session id

