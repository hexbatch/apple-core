# Inventory
Items in a store for sale, goods need not be physical or even real

Inventory is a set of one or more tokens, or token pools, that has a set of lot templates (not lots yet, but has the ingredients for them) 

The inventory has attributes, like media and text, to show what it is about

When a customer wants to put the inventory in a basket, or explore the price, 
the lot template closest in matching the requirements (bounds, weight, customer attributes, salesman handling this) 
is chosen.

Then the price can be shown.

When the customer puts the inventory in his basket, a new lot is made from the lot template,
* a sub-pool is made and put into the lot 
* or the inventory tokens are put into the lot

## Lot templates 

All the data for the lot, except for the set, is added to a lot template set, the set has an optional weight and boundary and salemen

Then, when lot needs to be made, the set to be sold is given to it and the closest match lot is made

### Price calculations

A script attribute can customize the attributes of a lot template, and that affects the price in the tokens (increase Blue by 3, reduce red by 5)