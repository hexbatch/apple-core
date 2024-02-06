# Selling

Sets up a sales flow that tracks different sales events from customer wanting to buy, to buying, to delivery, to issues, to feedback


* Selling starts with the intent to buy, with making a basket 
* The basket is sold at the same time, and this basket tracks the other sales lifetime 


## Basket 

Something for sale has a lot set up in the marketplace, it cannot be an auction. However, it can have other limitations and options set.

When a user wants to buy, he creates a basket set that contains one or more lots. These lots must belong to the same seller.

A user can have many different baskets. 

A basket can be set to dissolve or do other things based on attributes.

## The sale

When the user wants to buy, offers are made on the marketplace and the owner has the offer accepted for him.
The offers are put in the basket, along with the elements that were transferred to him.
A delivery of goods element is also put in the basket.

## Transfer of goods

If no transfer of goods needed, then the delivery of goods element is marked as done

If this is a digital download, then the delivery of goods has different series of steps than a physical transfer

## Finalization of the sale

if all is well and good, then the sale is marked as final with a complete delivery of goods.

A review set up is made, with those elements put into the element set of the basket

## When problems happen

Issue elements are put into the basket, these issues have a lifecycle

There is api methods for handling issues and resolving them


Sales can be agreed to be reversed before they are finalized, and reversed under a time or event condition.







