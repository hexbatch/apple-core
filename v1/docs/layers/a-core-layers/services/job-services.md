# Job Queue services

* will create a new job, put it on the queue
* will get a job from the queue, and execute it
* can iterate through the waiting jobs, can search for a waiting job
* can give details given a job id
* has a url callback for the function running the job to send update
* creates the long term storage for both the start of the job, and the output and issues for the job
* able to get stats for how many runs and errors any or all job functions are reporting
* can list the functions that can be queued, as well as some basic docs on each
  * These functions also list the core api calls going to be made   

Jobs are set up as functions that run elsewhere, and the data, in json format, for the job, is what is put in the queue

At a minimum the data in the queue has a job id, and a url to send job results back in json, the function to call, the user token.
Optional data can be provided in json

## Works with core permissions

* will count the api usage before the job is queued, and will only queue it if usage is ok by looking at function api usage vs allowed or remaining
