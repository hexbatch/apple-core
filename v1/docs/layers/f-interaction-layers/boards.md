# Boards

Are a type of agent that allow a bridge between outside communication and chat systems,  and the tokens and sets on the instance.

For example, if someone messages a user on a jabber server, an agent listening to that on some server or software somewhere 
 can talk to the instance here and create a token with that new message and put it into selected sets (inbox set etc.).

Likewise, if someone writes or creates a token, it can be made a message in a chat system or internet board.

Boards can also integrate multi-user group chats. Boards can be read only also, just delivering new notifications from the outside.

Boards will use chat networks. This allows integrated conversations on popular chat and boards which also tie into the instance here.

The boards layer is the api the agents use to do this. 

Also, chat agents can be registered here, as well as listed.

Some intended agents:
* an email agent
* a jabber agent
* something to use on both ios and android
* at least one internet board system somewhere


## Using chat and board libraries and display

* Chats can use public agents to connect to existing chat software
* Boards can use agents to use  board code

## Board sets

a board provides a set for people to read and write. A conversation will have one set, but a topics board might have a set for each topic, whose parent is the board root
