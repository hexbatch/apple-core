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
* calls `job:session.create_session`
* fills db row in with the job output
* return session id

# destroy  session
    session.create
* calls `job:session.destroy_session`
* deletes db row when get success

# get session
    session.get
* returns session data

# list sessions
    sessions.list
* returns all the sessions for the user

# list current area
    session.ls
optional args to do different pagination for set contents
* calls `job:session.ls`
* loads in command pallet using any loaded action services


# change session set
    session.cd
travels user to another set in this session
* calls `session.ls`
* puts current set into the session set history
* Changes this session to a new set



# do action
    session.action
* sends a filter event that the plugin can listen to, and that plugin can run a job (will wait for the job) or do something else
* will add in the filter response to the data returned. 


# Jobs

## job:session.create_session

Creates what is needed for a user session to start

Input data:
* user id, auth token, name of session, id of session

Core calls:
* list of core calls

Return data:
* session data to store, includes the id passed in, and the name


## job:session.destroy_session
Destroys the resources from a user session

Input data:
* session data, auth token

Core calls:
* list of core calls

Return data:
* session id


## job:session.ls

lists the contents of a set a visitor has his session in
todo list the contents, and provide a way to get more if too much for one pagination (with extra args here for what to list)
see user discussion

