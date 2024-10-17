The layers are thin wrappers to the core.

# Agents
* Oauth agents (scoped to path(s) and namespaces). Agents are logged in as the ns doing stuff.
  * thin message/or communication layer for agents that send out mail and messages (defines types) 

# Rates (depends on agents)
* Set core limits, set limits on this api. set limits for specific things.

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

# Security
* encrypting data written to elements
* wrapping type,element transfer with signed types and elements
* using https only, and other safeguards than those in the core, for server to server communication
* Servers using this will communicate with other servers using this layer

# Groups
* Groups have content types, these all inherit from the group content type. 
  * There can be unlimited sorts of content. 
  * Content can be public, protected, private
    * public is seen by non-members
    * package is seen by members of this group and child groups
    * private is only seen by members here
  * Content families, or individual elements of content, can be organized with tags.
  * Tags can be made by admins 
    * there is an additional level here, admin-only, so admins can do adminish stuff and can keep notes 
    * tags are sets that content can be put in and out
    * there can be sub tags
  * Actions can be added or removed by member actions on the content (upvotes, replies, consensus, sending content to elsewhere, changing content)
    * core mechanics on this: 
      * (each member reaction is a type combining the member type and the action type, so actions can only be done once  )
      * Action chains (like message chains or boards or sequence of events) is done by nested sets
* Groups have moderators over some or all of the group content, they can delete or edit some or all. 
  * Admins give permissions to the moderators.
  * Moderators can assign and/or remove none or some or all tags
* There are regular users, moderators and admins.  
  * Members can make friend lists of other members in the groups 
* The group definition, users, moderators, admins, content is in sets with elements
* Groups can send their types to the sets of some or all members at once
* Members can send messages to their friends or admins or moderators
* Groups have their own home set where moderator and admin elements are sent to them from the public or members or themselves
* Groups can define projects and provide structure
* Groups can be nested, that is there can be parent and child groups, 
  * the parent can moderate the children but the children only have protected access to the parent content and actions
  * user management on this layer is a group, all other groups made on this server is a subgroup to this one

# Remote caching and verification
The core allows any remote to be called
* This can be a proxy server for some or all remotes
  * Moderator can decide if using proxy 
* Can set up caching rules to remember calls based on time, user,ns,type,element,set
* Allow moderator to review remote urls
  * remotes that are blocked return failure code when used so no need to adjust anything in core 
 
