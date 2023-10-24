# Coding with tokens

There can be listeners, that listen to changes, and they change tokens, which can set off other listeners.
As the tokens drift between sets and instances, there can be chains of these event listeners and token changes.

But tokens can also interact with other tokens directly, in a set, and there can be loops and conditions and values exchanged.
These interactions can exist in one set or many, and these interactions might want to require catalysts, other tokens that tell them to start doing this.
Catalysts can also speed up the interactions, or rate limit them