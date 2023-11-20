# Movement in sets

Register a token here and it will move it around sets connected in relationships

When a token is placed in a set, it can sense if it should shift sets.
When it does that:
* it joins the idle movement set, which has an attribute on its token found only in the queue sets.
* If the actions allow it, then the token is put into this set.

In reality, this token is not really in a set, but that set joining puts it in the job queue for idle work,
and when the system gets around to it, will move the token to the best possible adjoining set.

The token is still in the set it wants to leave, and can still be interacted with.

No permission check needs to be done to get out of the idle queue.

But once the token it out, it needs to do permission checks via actions to see
* it can leave the first set
* if it can join the new set

If either check fails, the token will not be put back into the idle queue again while it belongs in that set

## Discussion

If a set has relations, then if there is a mix and the token finds a better attraction in a link or child or parent, it will move sets on its own.

A set has these measured by the token by having the current set and its neighbors summed up:  
The total "charge" of this token to a set is +1 for each attraction in a set, and -1 for each repulsion, this total number is the charge-per-set or -+

* -+ in the current set is 100%
* each immediate neighbor has its -+ set at 50%
* so if the current is at 3 and the neighbors are at -1/2 and 5/2 , the total charge for the current set is 5, and for the neighbors is 3/2 - 2  = -1/2 and 5 + 3/2 = 8 1/2 the token goes to the neighbor at 8.5

This movement is calculated when the token is first added, and whenever any new set links/relations are made/removed, and when new tokens are added or removed from the current or connected sets

internally, the counting takes place after all movement is done via an api command


# Movement api

The movement api has a public and a private part


## Private

the private is only handled by admins

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


## Public

register tokens, list what is registered, unregister them

Can set the same token to be registered multiple times, and it travels though different set paths at the same time.

Can set option to unregister token after it's stuck for a while

Can see what current set the token is at