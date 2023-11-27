# Marketplace

The marketplace allows more structure for transactions and contracts and pools.
It allows a common set of apis for all any kind of trade.

In the marketplace, one makes an offer, that offer can be for a specific user only. This offer can have a window
Then all that user has to do is accept the offer to start the sell (transaction or contract).
Or the offer can be for anyone to bid on, and then the offer user can accept the bid they want.
Bidding can be set for a time period.

All is sold as is with no refunds. As is. The selling layer will provide other stuff to marketplace sells.


## Lots

Lots are what are offered for sale.
lots can be created but not changed after the first bid on it is made, lots can have an expiring time or other bounds.

Each lot can have different prices (one or more types of tokens with the min or max which can be the same).
A lot must have at least one price.
But lots can have several prices.
Lots can have a set of requirements any of which can be met to choose a price.
Requirements can be bounded, so that different prices can be set for different areas or times or bid contexts.
It could be, that in some times, locations or path contexts - that there are different prices.

Requirements for choosing a price can also be done by groups of users added to each price.

Lots can have a range of times they can be sold or bid on.
Lots can be set to be deleted after no offers after a certain date.

Lot has a set which includes the tokens and resources that are to be traded.
The lo sets are inherited from a lot-type, and this is searchable.

## Offers

An offer is an attempt to buy the lot, for an offer to be created, it has to meet the price given.
Once an offer is made, the price cannot be changed. An offer can be retracted.
If the lot owner changes the price the user would have seen otherwise, later.
Then that does not change the offer already made.

An offer can contain text, media, contact details etc.

Based on the lot settings, the offer can be automatically accepted. Or the offer can be reviewed later.
If this is not an auction, and not set to automatically accept the first offer,
then lot owner can decide at any time to accept the offer, or can refuse all offers.
if there are not enough tokens for the offer when it is selected, the offer will fail.

### Auctions

When a lot is set for an auction, the seller cannot choose a winner until a certain time.

Auctions can be closed or open. If closed, the different bidders cannot see the other bids. 
If open, then anyone can see the bids.

A bidder can increase their offer.
There are remotes on the auction tokens that will start telling when someone is outbid, or other marketplace events 

## Award an offer

When the owner selects the winning offer, or if done automatically, then the resources in the lot set are done.
If this is tokens to be traded, then a transaction is made and agreed on.
If this is a contract template, then that template is rendered, and the agreement made and started.
if this is a pool template, then the pool is created and given to the user,
and the transaction to get the pool is created and done, and the contract for the pool is created

If the buyer does not have enough, when the offer is selected, the award will fail.

## Compare operations

Checks to see which offers can accept which prices at the current time

