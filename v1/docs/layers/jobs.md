# Jobs

Each layer api call is done by the jobs service.

This api also tracks job output and give notice.

Usually this task is executed as fast as possible, but if the user doing the call has the attribute of deferred-action set to true,
then the job is not done, until the user has a dynamic attribute set that references this job id. Then that attribute is removed and the job is executed.


a job can update its status using the job reference, only users who have the job-write role can use this.

job metrics can be queried, only users who have the job-read role can use this

job metrics allow hooks to be added to allow for events below


## Job Queues

Because there is reliance for executed javascript, as well as some db intensive operations.
Then some operations, if not all, should be done by a job queue, and the api caller should get back a callback reference
and if the api caller provides a url, or another form of callback, then the api will let them know when its done.

The core api does not do callback, but the next layer api will, and what the layers will do is set up some nested operations into a job queue.
The operations will have ties so that they are done in order, and the needed values from the yet to be executed ops are fed into the ops waiting for them.
For example, when making a new token, then doing something with it, like putting it into a set.

So the job data should have both the user that is logged in at the time, and the operations are done in the context of that user, and the callback reference and url.
This implies that the user should have a token to be used, when calling the core api. And the token should expire at the end of the job.
This means that the core api should use Bearer tokens, and have the api to revoke it


* see https://swagger.io/docs/specification/authentication/bearer-authentication/
* https://laravel.com/docs/10.x/sanctum#api-token-authentication

### Polling or callback or both

The callback does not need to be defined, instead, there is an api call to get the results using the job reference.
This job data/status data is only seen by using the reference and if the logged-in user is the one who made the reference, or the user who had the api done by permission
This implies there needs to be a data storage for the job reference, and has the calling user, the operational user, the job status and job api call response data, and the callback url,
and whether the callback url call was successful or not.

This way there can be cron jobs to try the callback url later, maybe.

This also means there needs to be an api to update the job reference by the job. but that api should not be exposed to the public.
Instead, the job itself is logged in as its own user to the outer layers, and has its permission set to use this api.
Probably all jobs can be the same user. See internal api


### Metrics

Approved users can get some or all of the network metrics. The admin can allow some metrics to be public without login

