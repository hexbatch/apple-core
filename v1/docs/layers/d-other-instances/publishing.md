# Auditing

* Auditing provides an api for publishing details of any transaction to agents.
  * It provides an api for agents: for sending the data, and interfacing to the programs that use this

* Provides a way to record new types, who created them. If the types are not registered before, will add that info before the transaction

* Api for recording new users, and changes of basic info

## Info in the auditing

### transactions 

At a minimum the guids of each user and the tokens (and their types), and amounts of tokens is stored


### Types

At a min, the user and limited info about the type

## what is sent out?


Anything with certain attributes will be watched, and when a change happens, it will be broadcast

-----------------------------
-- Not sure how to best do this. How to best tell when attributes, on a watched token, has changed, been created or deleted?
-- is this a different layer?
-- add in mirroring layer and remote user layer to this d-organization-layers

-----------------------------