# Agreements and consensus

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

An agreement can be used once or many times to power an api, by being the decision set to decide if it's going to be used by an operation.
This is done by setting up an action to listen to the event of being used as a switch for an api.

Agreements can be used to do actions for another user (such as an org or regular user) 
But agreement layer by itself does not decide which actions or api calls allowed. To limit that or times used, use the deferred layer. 

Agreements are marked as done when all parties mark their part of the agreement as done. In this way, agreements can be like milestones.
Agreements can be chained, so that the next agreement is only active when the previous agreements are completed. There can be any number of previous agreements and they do not have to be
related. Also. some of these agreements can already be done.

however all agreements depended on are part of the agreement upfront before anyone signs, and the dependencies cannot be changed after the first signing.

# Remote agreements

Agreements on this instance can depend on agreements completed on another instance. Agreements can be public and published.
If a wrapped agreement is used, then the mirroring has to update its condition to finished before any dependent agreements here are started.
So, this is just like a local dependent agreement, just the signers here cannot update that status,
but must do it on the other instance (either manual or part of a process done in their user there)

Agreements do not have to be public or published, but if they are published then can be used as a basis for other agreements on other servers, and there is a record of that

# Agreement logic


## agreement if else 

If an agreement is not completed by some time or future condition of another agreement. Then, an alternate agreement, and the terms of it happening, can be agreed on in the first agreement

Agreements can be put into if else conditions, when first agreement succeeds, this will will mark the other agreement as failed.
Or, if the first one does not work out, the second agreement will be able to start.

This can be done with multiple else if where there can be unlimited fallbacks.
Any one agreement here, finalizing, will result in closing out all the other agreements as failed.

## Multitask survivor

A number of events start out at the same time, the first one to succeed will mark the others as failed

## Looping agreements

Set one or more agreements as the loop control variable, all the agreements will start (single, block of, survivor, if else) and be attempted to be executed once
When each of those agreements are finalized, then will look to the agreements in loop control,
    if all the agreements there succeed , then the loop is done again, repeatedly, until one control agreement fails

##  Ancestry

Agreements can have a block of agreements be done first, and then either all or one of them has to succeed, or one or all fail (choose which of 4 conditions)
will propagate to start the agreement waiting on them.
