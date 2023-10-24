# Instances

Each instance of this api can interact with other instances

Using an agent, a user or token from another instance can travel to known sets inside the other instance.
These agents have their own native tokens in the destination set, and then a remote session can happen that is run just like a local session.

Instances should have a welcome shell in the list the instance gives when asked (instance layer)

## Tokens representing instances

Instances can be users in another instance, and can share sets. Users can find instances to go to in these sets. Instances can also discover each other this way too.