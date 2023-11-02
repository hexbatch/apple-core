# Movement api

The movement api is only handled by the same servers as the user admin api (localhost or private network range)

* Gets queue details
* Clears some or all of the queue
* Runs queue


| Method | Path                     | Route Name | Operation                     | Args                               |
|--------|--------------------------|------------|-------------------------------|------------------------------------|
| get    | movement/queue/stats     |            | returns stats of queue        |                                    |
| get    | movement/queue/list      |            | returns page of queue info    | maybe iterator                     |
| post   | movement/queue/run       |            | runs queue                    | optional id list to just run those |
| delete | movement/queue/delete    |            | deletes one or more queue ids | queue id list                      |
| delete | movement/queue/clear_all |            | clears the queue              | queue id list                      |

Queue Info:
    
    queue id:
    token waiting: id
    set from : id
    when put in queue: timestamp

Queue stats:
    
    total:
    oldest:
    newest:
    average_age: