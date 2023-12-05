# Mirroring

Related to the publishing, provides some apis to allow outside programs to tell this instance when something changes on another instance

When it gets info, it will see if this is for 
anything with a wrapper type parent.
If so, then updates

It can connect to different sources, and has a way to see if one or more of these sources is telling different info.
If the info is too different, then the watched tokens are not updated, or the updates are rolled back

Basically, follow selected token attributes and ownership.

If user Mary has 5 tokens from another instance, and they belong to her.
When she trades them elsewhere, then it should be that the tokens no longer belong to her on this instance.
If the new user of those tokens is not followed on this server, then those tokens simply are removed and destroyed here

A type's token can be followed with some of its attributes.

A token is only followed if the user here, or a followed user, owns them

# Discussion

Allows the usage of some other network and protocol and other software to link the instances together.
For example, the publishing will tell the other stuff that there is a change, and the other stuff will inform here at the listening when something is changed

## Notice of things being listened to elsewhere

Other instances can use the publishing layer to announce when new things are being listened to, then can add in attributes here, or make some list to watch


# Wrapping

A wrapped token is like a smart pointer, it's attributes echo what is known about the token, none of them are writable on this server.
The attribute ids are the same, but the values are only constant

its type is from the wrapped type, made by the layer.
Wrapped types have same id, and have read only attributes reflecting the followed attributes
The owner of a wrapped type is always the same user, which is a user created by this layer
Wrapped types cannot have new tokens created from it except by the owner.
Wrapped types have standard attribute that points to that type in the original instance

Some attributes in the wrapped type can be marked to always get the live info, this is done by making the attribute values be remotes that get the info


When new tokens of this type are found, by listening to the followed users from other instances,
and they are owned by people on this instance, then those tokens are made from the wrapped type.
The new tokens from this wrap have standard attribute that points to that token in the original instance.



//note need a way in the layers to quiz individual tokens and types, in read only. Perhaps in the grants layer