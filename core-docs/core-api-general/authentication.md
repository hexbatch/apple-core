# User authentication

All api, except getting a token, and getting standard attribute info, require a token (so the user is logged in).
The core is not really exposed to the public though, and the outer layers can allow un-logged in people to see stuff, using some user for public stuff

A user can  have many different bearer tokens that are valid. Once the user gets his bearer token, he can use an api call to get another one.
This is good to use with jobs.
A bearer token can be generated, to use with jobs, so the pw does not have to be sent with the job data.
But the jobs should have just temporary tokens they delete when done.