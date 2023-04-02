# Auction system

## Introduction

Specification of functional requirements as part of computerisation of the product sale process based on the auction mechanism.

## Business processes

---
<a id="bc1"></a>
### BC1: Auction sale

**Actors:** [Seller](#ac1), [Buyer](#ac2)

**Description:** Business process describing a sale by the auction mechanism.

**Main scenario:**
1. [Seller](#ac1) offers the product at an auction. ([UC1](#uc1))
2. [Buyer](#ac2) offers a bid for the product that is higher than the currently highest bid. ([BR1](#br1))
3. [Buyer](#ac2) wins the auction ([BR2](#br2))
4. [Buyer](#ac2) transfers the amount due to the Seller.
5. [Seller](#ac1) transfers the product to the Buyer.

**Alternative scenarios:** 

2.A. Buyer's bid has been outbid and [Buyer](#ac2) wants to outbid the current highest bid.
* 2.A.1. Continue at step 2.

3.A. Auction time has elapsed and [Buyer](#ac2) has lost the auction. ([BR2](#br2))
* 3.A.1. End of use case.

---

## Actors

<a id="ac1"></a>
### AC1: Seller

A person offering goods at an auction.

<a id="ac2"></a>
### AC2: Buyer

A person intending to purchase a product at an auction.


## User level use cases

### Actors and their goals 

[Seller](#ac1):
* [UC1](#uc1): Offering a product at an auction

[Buyer](#ac2):
* [UC2](#uc2): Making a bid for a product offered by Seller

---
<a id="uc1"></a>
### UC1: Offering a product at an auction

**Actors:** [Seller](#ac1)

**Main scenario:**
1. [Seller](#ac1) reports to the system the willingness to offer the product up at an auction.
2. System asks for the product data and initial price.
3. [Seller](#ac1) provides product data and the initial price.
4. System verifies data correctness.
5. System informs that the product has been successfully put up for auction.

**Alternative scenarios:** 

4.A. Incorrect or incomplete product data has been entered.
* 4.A.1. informs about incorrectly entered data.
* 4.A.2. Continue at step 2.

---

<a id="uc2"></a>
### UC2: Making a bid for a product offered by Seller

**Actors:** [Seller](#ac1), [Buyer](#ac2)

**Main scenario:**
1. Buyer reports to the system the willingness to buy the product at an auction.
2. System asks for kind of product.
3. Buyer provides kind wanted product
4. System informs Buyer about available products
5. Buyer choose one product
6. System asks about the size of bid for a given product
7. Buyer provides size of bid
8. System verifies data correctness
9. System informs that the bid for the product has been succesfully made.

**Alternative scenarios:** 

4.A. Lack of product, that Buyer wanted to make a bid 
* 4.A.1. System informs about lack of wanted product
* 4.A.2. Continue at step 2

8.A. Bid made by Buyer is less than initial price or is less than already made bits between step 4 and 7 or the product was sold between step 4 and 7.
* 8.A.1. System informs that bid is less than initial price
* 8.B.1. System informs that bid is less than other bids
* 8.C.1. System informs that product is already sold
* 8.ABC.2 Continue at step 4

---
<a id="uc3"></a>
### UC3: Completing the transaction at an auction

**Actors:** [Seller](#ac1), [Buyer](#ac2)

**Main scenario:**
1. System close an auction for a given product, that means it closes an option of offering other bids.
2. System informs [Seller](#ac1) of the given product about the highest winning bid.
3. System pass money from mentioned bid to [Seller](#ac1).
4. System asks [Seller](#ac1) to provide the product to the winner of the auction.
5. [Seller](#ac1) provides a given product. 
6. [Buyer](#ac2) collects product. 

**Alternative scenarios:** 

2.A. System informs [Seller](#ac1) about lack of bids for the given product. 

---

## Business objects (also known as domain or IT objects)

### BO1: Auction

The auction is a form of concluding a sale and purchase transaction in which the Seller specifies the starting bid of the product, while the Buyers may offer their own purchase offer, each time proposing a bid higher than the currently offered bid. The auction ends after a specified period of time. If at least one purchase offer has been submitted, the product is purchased by the Buyer who offered the highest bid. 

List of products offered by sellers with their description and initial price and specific time ending a given auction for this product. 

<!-- ### BO2: Product

A physical or digital item to be auctioned.

### BO3: Initial price

The starting price for the product at the beginning of the auction. -->

### BO2: Bids

The amount of money that the buyer is willing to pay for the product.

### BO3: Buyers

List of Buyers, when Buyer is a person or entity who is interested in buying a product at auction.

### BO4: Sellers

List of Sellers, when Seller is a person or entity who is interested in selling a product at auction.

## Business rules

<a id="br1"></a>
### BR1: Bidding at auction

Bidding at auction requires submitting an amount higher than current by a minimum of EUR 1.00 and is higher than the initial price and any previous bids. Except that a buyer can only make a bid for a product if it is available at the auction.

<a id="br2"></a>
### BR2: Winning an auction

Auction is won by [Buyer](#ac2) who submitted the highest bid before the end of the auction (time expires).

<a id="br3"></a>
### BR3: Putting product an auction

A [Seller](#ac1) can only offer a product at an auction if they provide complete and correct product data and an initial price.
The system must verify the correctness of the data provided by the [Seller](#ac1) before putting the product up for auction.

<a id="br4"></a>
### BR4: Lose at an auction

Auction is not won by [Buyer](#ac2) who submitted bid if it didn't submitted the highest bid or it didn't submitted bid before the end of the auction. If the product is no longer available at the auction (e.g., it was sold), the system must inform the buyer of the status and allow them to choose another product or exit the auction.

<a id="br5"></a>
### BR5: Losing at an auction

If a bid is made that is less than the initial price or any previous bids, the system must inform the buyer that their bid is invalid and allow them to modify their bid or exit the auction.

## CRUDL Matrix


| Use case                                  | Auction |Bid  | Buyer | Seller |
| ----------------------------------------- | ------- |   -------- | ----- | ------ |
| UC1: Offering a product at an auction     |    C    |  |  | C |
| UC2: Making a bid for a product offered by Seller                                       |   R   | C,U | C | R |
| UC3: Completing the transaction at an auction                                       |   R, U   | R | R | R |

