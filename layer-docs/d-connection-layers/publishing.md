# Publishing

* It provides an api for agents: for sending the data, and interfacing to the programs that use this

* Provides a way to record new types, who created them. If the types are not registered before, will add that info before the transaction

* Api for recording new users, and changes of basic info

## what is sent out?


Any token with certain attributes will be watched, and when a change happens, it will be broadcast

When something is made public, that is a decision by someone who can write to the token.
In that case there is are two value_change_filtered listeners for the token, that first filters anything to update via a javascript,
then that is passed to the remote that talks to this api


## Info in the publishing


At a minimum the give guids of each token published, its user, its type, the name, and key values of the attributes that are readable by the public


### Types

At a min, the user and description about the type, at least the first sentence


