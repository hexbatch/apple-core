# Stores

Stores sell inventory

Stores have an api to help make inventory discoverable and answer questions before purchase

Stores can be run by a single user or an organization

Stores have a staff

Stores have a reputation and feedback boards

## Managing inventory

Stores set up an inventory, with levels on hand, and sets the costs per bounds (or also per salesman).

Stores can set up inventory with display and media.

Stores can set up inventory variances

Stores can set up delivery rates for inventory

### Discoverable Inventory

Stores can make categories. They associate inventory with these. 

Similar inventory (like different colors of coats of the same type) can share the same categories

When people search vian elements or attributes, which are included in these categories, the store can respond to a list of inventory and a salesman, or choice of salesmen.

Inventory can be searched with the requirement of a certain selection of salesmen to handle it (asking for someone specific to help with this)

### Making categories

A category is a set that has inside of it element of attributes, as well as inventory elements to be grouped here, as well as salesman elements. This makes it searchable

## Store staff

Users can be in the store staff group. 

Each user is given a store salesman element that inherits from the salesman element and this store.

These users are called salesmen.

Each salesman can have a location or time schedule, or even a search path boundary (to only answer certain searches in the categories or other element searches)

### Salesmen roles

Salesmen can be there to answer questions, do delivery, or both

### Salesman commission

Stores can be automatically made to give a flat or percentage commission, or both, to a salesman who makes a sale

### Salesman reputation

Each salesman at each store has his own reputation made by customer feedback

## Store chat

Stores use the boards api to set up private chats about inventory, and these chats also extend to sales delivery and issues. More people can join the chat as necessary/ 
