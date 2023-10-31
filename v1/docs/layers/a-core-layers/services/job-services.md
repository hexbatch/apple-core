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

* each job function is defined by a plugin
* job functions may be pulled in from other repos
* each job function will call `core.user.auth.destroy` at the end to destroy its token!

# This is the only microservice that calls the core api indirectly and directly

Flow for placing a job and getting data and status back via url:
* caller calls the `job_services.do_job` with the user, function name, and data and a url and the wait flag set to false or unset

Flow for placing a job and waiting for it to finish
* does the above, but with the wait flag set to truthful 

# console job task for waiting
* pass in user and function name using args
* pass in data either with arg for data or arg for file name
* task will complete when it gets back the callback for finishing
* then the task returns the printed json of all the task output

# API

## do job
    job_services.do_job
* if the wait flag is set, then call the job task for waiting and return when it does
* otherwise call `job_services.start_job` and return the job id it gives on return
    

## start a new job
    job_services.start_job
* makes new db entry for a job
* takes all the data given here, (the user, the function name, the data to be used in the call) and puts that in a queue
* returns the job id

## process start job queue
* this reads from the queue for starting jobs, and calls `job_services.create_job`

## create a new job
    job_services.create_job
only called in the queue for starting new jobs

  * calls `permissions_core.can_i_do_this` for all the listed api calls in the job, if user cannot then return with data explaining (or throw)
  * calls `user_services.get_basic_user_auth`
  * calls `core.user.auth.create` for auth token put in
  * makes new db row for the job
  * queues this with given data, and callback url


# job status hook called from the job execution
    job_services.update_hook
  * update job status
  * if this job is not done return
  * if provided callback url call that
