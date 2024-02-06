# External user


When a user element from another instance enters this instance for the first time, they do not have to register or manually create a new account.

Instead, the user provides their home instance, and a new user is automatically created that inherits both from the user type and the wrapped type.
The user type and the wrapped type are both parents of this new user type.
This server then sends a message through the auditing layer that we are now watching this user element.
There are the same things watched between servers, but can add in extra attributes to also watch

The wrapped user cannot edit their attributes or personal group on this instance, only on their own instance. The changes are propagated here to this instance.
(Their user creation, also inheriting from the wrapper, disallows their editing of their attributes.
The wrapper has listeners that reject changes if the one doing it is not in a group)
However, otherwise this is a normal user, when they do transactions here, or other things that should be followed and mirrored on their own instance, 
the instance's auditing layer broadcasts that, and the instances auditing layer will get it through their auditing

It uses the mirroring layer to update the user element. 

The external user layer can decide that some of the user's elements are worth listening to also, if that is the case, it will send that followed list to the listeners



