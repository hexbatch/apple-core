Agreements and consensus

This is a way for people or scripts to agree on something

    Set up something that only written to if all users in a group write the same value... possible to do only in layer?
        - but this can be done via a set, and have selected people write to the set, and then do an agg function to count their token, and then match the value,
           if value matches then write to an attribute on a token whose permissions is not allowing the users submitting values to write directly


Make agreement set that has to have the users put their user token in, and the value or consensus is reached

Agreements can expire after a certain time, or have other conditions before a user can put their token in,
such as contents of tokens in a set done after a set or mutual operation is done

An agreement can be made to be decided on, but not done, until conditions.
Conditions can be previous agreements

Agreements can have different attribute in their set token designating if ready to be agreed on, or voted, or if waiting, or if everyone did that

The creator of the agreement can delete it only if nobody has agreed yet.

A person can remove their user token if decide they changed their mind.

An agreement  can be set up to have a delay or datetime to do the transaction after all signed

Agreements can be set to allow a percentage of users to decide, or can be set to allow different users to have different weights

Agreements can be cancelled later by any user removing his token, or having it be set to a percentage of users or weights. A cancelled agreement is an empty set

An agreement can be used as the set to decide to do a repeating api.

Agreements do not have to be public or published, but if they are published then can be used as a basis for other agreements on other servers, and there is a record of that
The internet layer will publish agreements

An agreement can be used once or many times to power an api, by being the set to decide if it's going to be used by an operation.
This is done by setting up an action to listen to the event of being used as a switch for an api.

Agreements can be used to do actions for another user (such as an org or regular user) by using the deferred. 



