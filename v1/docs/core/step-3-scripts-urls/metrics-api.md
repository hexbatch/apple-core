# Script and Remote metrics

metric api defined at

The metric api is only handled by the same servers as the user admin api (localhost or private network range)


There will be a need for people to see how often things are called, and any errors.
Data sent to and from a resource is not seen here.


| Method | Path            | Route Name | Operation                               | Args                       |
|--------|-----------------|------------|-----------------------------------------|----------------------------|
| Get    | metrics/scripts |            | gets a paginated list of script_metrics | can pass in filtering info |
| Get    | metrics/remotes |            | gets a paginated list of remote_metrics | can pass in filtering info |


Filtering data can be:
* owner
* script or remote  name
* times (range)
* status (depends on the type of resource)
* ordering_array: order by  time, status, owner

## Script metrics

    name of script running
    owner of script
    how long ran ms
    when ran
    errors when running
    warnings when running

## Remote metrics

    name of remote running
    owner of remote
    how long wait ms
    when ran
    http status or exit status


If someone can see a script, or a remote, it will show up when this is called