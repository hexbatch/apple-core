# Script and Remote metrics

metric for scripts and remotes can be seen via console tasks
Data sent to and from a resource is not seen here.

What will be seen is times and cpu and similar

| Task           | todo | Operation                               | Args                                                                 |
|----------------|------|-----------------------------------------|----------------------------------------------------------------------|
| script_metrics | *    | gets a paginated list of script metrics | optional filtering, ordering and also choose next and previous pages |
| script_metrics | *    | gets a paginated list of remote metrics | optional filtering, ordering and also choose next and previous pages |


Filtering data can be:
* owner
* script or remote  name
* times (range)
* status (depends on the type of resource)

Ordering
* order by  time, status, owner

Pagination
* options for next, prev and start (default) (uses cursor stored in cache, key in file)

## Script metrics

    name of script running
    owner of script
    how long ran ms
    cpu usage
    when ran
    errors when running
    warnings when running

## Remote metrics

    name of remote running
    owner of remote
    how long wait ms
    when ran
    http status or exit status

# todo
* not done yet
