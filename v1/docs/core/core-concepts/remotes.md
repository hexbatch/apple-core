# Remote calls and using programs in the core

Remotes allow attributes to run a program, or make a call to a socket, or a private network, or make an internet call

These are run when the attribute is written to, or read from. There is some caching here, as well as limits, that can be set when the remote is defined,
so that the outside resource is not called too many times.

## Example
So, if I have a token that is about bears, and I have an attribute called bear-count. When I read it, it will get the info from the zoo in Washington state, and store that for a day

## Usages

Remotes allow extending what the tokens do.