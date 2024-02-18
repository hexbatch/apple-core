# Remote calls and using programs in the core

Remotes allow attributes to run a program, or make a call to a socket, or a private network, or uri

Remotes are called on event listening. And when certain attributes are read or written.
Remote calls can be cached at the global, user, type, action, attribute, or element level.
Remotes can impose rate limits, as well as caching rules when these are exceeded.

Several remotes for an api action can be called at once, these can be resolved together, 
and failure of some or all can be decided on by the logic of the api call.

## Examples
* So, if I have an element that is about bears, 
and I have an attribute called bear-count. 
When I read it, it will get the info from the zoo in Washington state, and store that for a day.
Then if before that day is out, I can read the attribute again, and it will return the data from the local cache.

* When I create an element, and that type has constructor events from two ancestor chains and the current.
Then, I can call all of them, and if anyone of them says no,or fails, that element will not be created.

* When I move an element to a set, and there are some listeners to deny it, and other listeners in the set to read it. 
Then I can call the event remotes, but only if one answers back and says no will I stop the movement.
Then I call the remotes that are toggled by the elements that want to read this value, I call all of them and do not care about the responses.

* I am displaying some sets on my webpage, and I set up a remote that executes on my page's javascript. This is a manual remote,
and I poll the api to find out when I need to fill calls out, I do that, and send back the reponse, and that api call proceeds.


