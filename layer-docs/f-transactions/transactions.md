# Transactions

The transaction layer changes ownership of elements after an agreement,
or series of agreements, between two or more people.

Each transaction  is limited to one user swapping a set of elements with another user.
Or moving elements from one set to another.

Transactions can be in many parts and swap more than one owner.
They are chained by agreement chains, but the transactions also reference a transaction parent.
So there are two parent chains, the agreement parent and the transaction parent.
Like any agreement chain, all the conditional agreements have to pass to get to the next ones.
A transaction failing also fails the agreement.

If in an agreement chain, the txn cannot start until the chain starts.

Due to allowing long pauses to complete a transaction, this is great for allowing multiserver transactions
These transaction chains can wait on a remote agreement to be completed.


The transaction layer makes an agreement to change ownership of elements.
* A previously made agreement can be passed as a conditional
* The agreement made here can be inserted into agreement chains to be executed or not later

There can be multiple parties to the agreement element. 
* The swapper users must be parties.
* One set can be empty, but not both
* The swappers have to be different users
* The agreeing users must include both of the swappers, but can include any number of other users
* The creator of the transaction can delete it only if nobody has agreed yet.
* Any party to the agreement can cancel the transaction before it runs.
  * Any party can remove their user element from the agreement before it executes, this cancels the transaction


After the agreement succeeds, the transfer will take place

Different options when making a transaction:
* Transactions can be set to be deleted after N time after no agreement is reached.



## Escrow

Escrow: Elements that have their ownership changed, but the entire transaction chain has not finished,
cannot change their ownership in a new transaction until that is done.
They are held in escrow, new/old owners do not have any special privileges,
but can read/change them as a non owning user.
The escrow status once the agreement starts the transaction.



## depositing

Each user getting ownership can designate a set the elements are placed in , once the transaction completes

# discovery

Transactions can be marked as public, when that happens, it is pushed to the auditing api

# Cancelling

Any of the users can cancel the transaction while still being processed, the elements in escrow are rolled back.
There can be a timeout for the transaction to go through too, and if not, then auto cancel


# Transactions depending on multiple agreements

A transaction can wait on any number of agreements to be finished, before that starts.
Agreements can be wrapped ones from other servers

public transactions and agreements can be used across different servers as dependencies of each other.

Private transactions cannot hop across instances, because it's not in the mirror/publish 


## mixing in remote transactions

Elements can only change ownership if both are hosted by the same instance.
However, transactions can be combined in different instances by using the listened to and published agreements being completed

* I can make an agreement to transfer some elements on Server X
* Then, when that agreement completes, the agreement here can start
* Then, server Y can listen to our local agreement completing, due to the transaction going through, and starts it own transaction chain

So, I can agree that elements A on server X have some equivalence to elements C on this server,and when I get elements A on X, I will do transaction in Elements C on here.
These chains can be extended indefinitely.
Completed agreements will pass things through automatically

but, things can mess up, and an agreement will not finish somewhere. If that is the case, there is a rollback clause in the transactions if there is no progress after X seconds


## Deadlock

It may not be possible to avoid certain deadlocks unless enforce no reuse of agreements or their dependent agreements in any transaction.
There might be some exceptions thought about later.





