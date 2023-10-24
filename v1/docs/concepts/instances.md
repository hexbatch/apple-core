# Instances

Each instance of this api can interact with other instances

Using an agent, a user or token from another instance can travel to known sets inside the other instance.
These agents have their own native tokens in the destination set, and then a remote session can happen that is run just like a local session.

Instances should have a welcome shell in the list the instance gives when asked (instance layer)

## Tokens representing instances

Instances can be users in another instance, and can share sets. Users can find instances to go to in these sets. Instances can also discover each other this way too.


## Shells linking instances

Instances can be hooked up in such a way that tokens entering a set automatically are set up with an agent to go to another set, and this can be one or two ways.
The tokens from the other instance can join a set and be sent back to the originating server. There can be networks of instances set up to have specific relations between each other,
and sessions and tokens can go from one to the other in some set order, or in a layout of relations.

### Each instance can have its own user account on another server

When instances connect, they not only set up user accounts for each other, so that they can interact more. 
But they also set up a way to allow users on each to visit the other without having to re-register or login

Once an agent is authorized on one instance to work with a user, the agent can visit other instances that the user's home instance has signed up, and do things there