# Communication

Are an api for connecting to agents for email, chat and communication systems. This ranges from bulletin communications to live chats to emails.
The agents convert any incoming to an item,

The user can reply to the item and then an action on that item has a remote that calls this api.
The api will talk to the agent for that service where the item came from, and have it send a response to the outside message system.
The response will be published on the service by the agent.


For example, if someone messages a user on a jabber server, an agent listening to that on some server or software somewhere 
 can talk to the instance here and create an element with that new message and put it into selected sets (inbox set etc.).

Likewise, if someone adds a child element to a parent item element, it can be made a message in a chat system or internet board.

Communications can also integrate multi-user group chats. Communications can be read only also, just delivering new notifications from the outside.

Communications will use chat networks. This allows integrated conversations on popular chat and communications which also tie into the instance here.


Also, chat agents can be registered here, as well as listed.

Some intended agents:
* an email agent
* a jabber agent
* something to use on both ios and android
* at least one internet board system somewhere


## Using chat and communication libraries and display

* Chats can use public agents to connect to existing chat software
* Communications can use agents to use  communication code

## Communication items

The communication api uses items api to record the messages and info, and to send that info to the users in the instance.

Some communication integrations it makes more sense to use a protected message set for chat or reply chains, for things like chat conversations, or message communication replies.
For example, a new top level email can be a new item, and the replies under it can be protected message elements in that message set.


## Agent networking

Each agent type, email or jabber, has a network type, as defined by this layer from a basic network type.
and each user account from a network inherits from the user type and the network type. This is called a communication-account type

When a communication makes an item, that item also inherits from the communication-account type
