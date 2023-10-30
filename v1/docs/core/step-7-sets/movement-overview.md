# Movement in sets

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
