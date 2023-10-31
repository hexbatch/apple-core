# Job Queue services

* will create a new job, put it on the queue
* will get a job from the queue, and execute it
* can iterate through the waiting jobs, can search for a waiting job
* can give details given a job id
* the function running calls back to here, so the job can update data
  * if here has a url callback for layer setting up this job, it will call that
* creates the long term storage for both the start of the job, and the output and issues for the job
* able to get stats for how many runs and errors any or all job functions are reporting
* can list the functions that can be queued, as well as some basic docs on each
  * These functions also list the core api calls going to be made 
  * functions can be listed in console

Jobs are set up as functions that run elsewhere, and the data, in json format, for the job, is what is put in the queue

At a minimum the data in the queue has a job id, and a url to send job results back in json, the function to call, the user token.
Optional data can be provided in json

## Works with core permissions

* will count the api usage before the job is queued, and will only queue it if usage is ok by looking at function api usage vs allowed or remaining

## Plugin driven

* each job function is defined by a plugin (committed to same repo in the plugins folder)

# API

## create a new job
    job_services.create_job
  * checks with the core permission service to see if this can be made
  * gets a new token from the core for the user, using the token stored in the user-services. Does not store new token in layer db


# In each job
    job_step.destroy_token
  calls the core to destroy that token
