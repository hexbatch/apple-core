# Transactions

The transaction layer changes ownership of tokens after an agreement, or series of agreements, between two or more people.
Transactions can be in many parts and swap more than one owner. All have to succeed for the ownership to be changed for any

The transaction layer makes an agreement to change ownership of tokens.
There can be multiple parties to the agreement token.


The creator of the transaction can delete it only if nobody has agreed yet.
A person can remove their user token if decide they changed their mind.
A transaction can be set up to have a delay or datetime to do the transaction after all signed
The transfer can happen after all agree.
While waiting, anyone who previously agreed can remove their token from the agreement.

Transactions can be set to be deleted after N time after no agreement is reached.
Transactions can be set to allow reuse by doing a new agreement, all agreements to a transaction will be linked to that


The tokens exchanged here can be more than trading, it can be part of mechanics and set new relationships

The transaction layer allows nested transactions, and each transaction can be between different users of the agreement,
If any of the nested transactions do not work out then the transaction does not happen.
And ownership of all is rolled back, the tokens removed from escrow.

The nested transactions work by using nested agreements.


Escrow: Tokens that have their ownership changed, but the entire transaction chain has not finished, cannot change their ownership in a new transaction until that is done.
They are held in escrow, new/old owners do not have any special privileges, but can read/change them as a non owning user.
The escrow status once the agreement starts the transaction.

Due to allowing long pauses to complete a transaction, this is great for allowing multiserver transactions
These transaction chains can wait on a remote agreement to be completed.

## depositing

Each user getting ownership can designate a set the tokens are placed in , once the transaction completes

# discovery

Transactions can be marked as public, what that happens its pushed to the auditing api

# Cancelling

Any of the users can cancel the transaction while still being processed, the tokens in escrow are rolled back.
There can be a timeout for the transaction to go through too, and if not, then auto cancel


# Transactions depending on multiple agreements

A transaction can wait on any number of agreements to be finished, before that starts. Agreements can be wrapped ones from other servers

public transactions and agreements can be used across different servers as dependencies of each other.

Private transactions cannot hop across instances, because it's not in the mirror/publish 


## mixing in remote transactions

Tokens can only change ownership if both are hosted by the same instance.
However, transactions can be combined in different instances by using the listened to and published agreements being completed

* I can make an agreement to transfer some tokens on Server X
* Then, when that agreement completes, the agreement here can start
* Then, server Y can listen to our local agreement completing, due to the transaction going through, and starts it own transaction chain

So, I can agree that tokens A on server X have some equivalence to tokens C on this server,and when I get tokens A on X, I will do transaction in Tokens C on here.
These chains can be extended indefinitely.
If they loop, then the completed agreements will pass things through automatically

but, things can mess up, and an agreement will not finish somewhere. If that is the case, there is a rollback clause in the transactions if there is no progress after X seconds


## Deadlock

It may not be possible to avoid certain deadlocks unless enforce no reuse of agreements or their dependent agreements in any transaction.
There might be some exceptions thought about later.





