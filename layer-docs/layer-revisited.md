The layers are thin wrappers to the core.

# Agents
* Oauth agents (scoped to path(s) and namespaces). Agents are logged in as the ns doing stuff.
  * thin message/or communication layer for agents that send out mail and messages (defines types) 

# Rates (depends on agents)
* Api limits, and ways to modify those. User has a set of elements that keep track of api calls, one element per api.
The core is not designed to restrict or protect api endpoints. The rates give protections and allow later transactions in the business

# Community (depends on agents)
* Agreements: two or more people vote to do something, can have different thresholds, success unlocks or allows something.
Agreements can be cancelled affecting stuff, or can be one shot things.
* Organizations: ownership is shares, the % of shares each user has weighs in the agreements, 
these can make certain sorts of actions now and in future possible, by one or more owners (decided). Very adjustable.  

# Business (depends on community)
* Transactions: swap ownership/usage of sets containing elements
* Contracts: Repeating or time sensitive transactions
* Element pools: transactions can trade rights to make elements and under terms (including locations, times, amounts)
* Auditing:  record keeping/verification of transactions

 
