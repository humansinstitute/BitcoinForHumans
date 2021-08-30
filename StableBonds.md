# Stable Bonds

## An approach to community based bitcoin backed stable currencies (like a stablecoin but not)

An alternative idea for creation of stable coins.  The core concept is that instead of utilising a “bearer token” backed by collateral (in a bank or a smart contract) we utilises markets and long / short preference to manage stability.  

The mental model I choose to think about this is to consider stable bonds as a bitcon collateralised bond market.  

The goal is to do this in a trust minimised peer to peer architecture.

This would allow any individual to elect to store a percentage of their bitcoin wealth in a "stable" form (defined as approximately pegged to the market exchange price of BTC/USD), with an eventual goal of reducing the volatility risk inherent in the earning and storing BTC when living in a hand to mouth fashion.

I believe this would allow easier adoption of bitcoin, where it is most needed, if inidividuals could earn "USD on native bitcoin rails" and then engage in native swaps to bitcoin.

*(This is very much a draft and there are a lot of edge cases to talk through I think, but the basic concepts and I would welcome discussion - Pete)*

---

## Overview

![Overview diagram](https://raw.githubusercontent.com/humansinstitute/BitcoinForHumans/master/assets/stablebond-overview.jpg)

The proposed stack would include a client which sits on top of a lightning network and bitcoin network node. 

The client will require functionality to manage several scenarios.

* Order matching: How larry met sally. 
* Reputation: Sally wants to take a market offer from Larry and is assessing his reputauion as a peer. gning and enforcement of DLC.
* DLC Management: Negotiation, si
* Exposure calculations, 
* Automated rolling of bond contracts. 

Stablebonds referred to as bUSD represent a fixed amount of USD exposure, created as a synthetic instrument betweeb two peers in a discrete log contract. This is achievable now, however, there are several design considerations when looking to scale this to more people and create a tradable (i.e. for products and services) curency.

The purpose of this design is to facilitate a number of use cases such as: 

* UC001: Sally has no bank account but would like to sell goods / services and receive $USD (or equivalent) to her phone. 
* UC002: Sally would like to hold USD securly outside of a bank account. 
* UC003: Sally would like to be able to create and hold bitcoin in a savings account under her control without a bank.
* UC004: Larry would like to go even more long Bitcoin without a counterpary.    

## Creation of Stable Bonds
Instead of the traditional approach of issuing bearer tokens representing bUSD we instead enter into a short term bond contract which is denominated in USD and collateralised on both sides by BTC. 

This allows any individual or organisation to “mint" bUSD by entering a DLC contract in a peer to peer contract which goes short bitcoin against USD over a 4320 block (1 month) or 144 block (1 day) period.

This person now has an stable balance which can be displayed in a wallet application for ease of use. At the end of the period this will settle back into bitcoin.  Should the user want retain a USD balance they would roll forward the bond. 

This of course requires a liquid market for bUSD offers, or put another way this requires there to be a liquid market of people who want to go levered long bitcoin :).

### Early exit from a StableBond

At any time, this person could agree with their counterpart to “roll” this contract forward (this is a 2-of-2 multis so can be collaboratively closed and reopened) or failing that the contract settles and they can simple open up another contract to maintain their CYM balance, indeed the wallet could be instructed to do this automatically.
 
Ideally this contract would also have a "closeing term" which setles the contract at that time with a small fee paid to the "maker".

Let’s wave our magic wand and assume we fund and settle these contracts on lightning.

### Rolling a Stablebond


### Secondary CYM Market

The idea here is that if we can establish DLC contracts that are routable between different users then we can now “sell our CYM” into a secondary market for SATS! 

So for instance lets say I agreed a 1 month contract for bitcoin against CYM - which at any point in time is worth approximately XYZ amount of sats currently referenced by the price feed. 

If we assume that right now we have a contract worth 100,000 sats we might expect to be able to trade out of that contract for up to 100,000 Sats if there is an active market of new users wanting CYM. 

This market would require an order matching service and to facilitate the escrow services for the transfer and many different trust models could be utilised from centralised actors to peer to peer - some more thought required here. 

However what this really allows is to people to enter and leave these contracts at will, assuming there is a liquid CYM/BTC market and history tells us that “stable coin / BTC” markets tend to be pretty liquid. 

### Spending CYM

The spending can leverage lightning as the settlement layer. Which means our erstwhile user now needs unencumbered bitcoin on lightning! But First let’s consider the “spending transaction” not from the point of view of a sat moving through the network but as a particular set of outputs post transaction.

Example:
	- Start Alice has 10 CYM, Bob has 0 CYM.
	- MAGIC HAPPENS
	- END Alice has 5 CYM, Bob has 5 CYM. 

If each CYM were an individual “token” Alice would simply give Bob five CYM and we get the outcome. But there are other ways to achieve this outcome. 

Specifically the “MAGIC HAPPENS” could be one of a few different flows, which all arrive at the same conclusion if we assume our Secondary CYM market is indeed liquid:

**Option 1** 
	* Bob is present and identifiable in the secondary market
	* Alice takes her 10 CYM contract to the secondary market and sells the 10 CYM contract
	* Alice establishes tract aga 5 CYM long contract. 
	* Alice establishes a 5 CYM short contract to Bob.

**Option 2**
	* If Bob actually wants to sell in CYM but receive in Sats.. 
	* Alice Sells her 10 CYM contract for 5 CYM and XYZ Sats. 
	* Alice routes sats to Bob over lightning sett;ling the sale.

**Option 3**
	* As 2, but Bob wants CYM so add thee step
	* Bob then Bob Mints a new 1 month CYM contract with sats recieved from Alice for 5 CYM. 

Ideally I’d expect you’d want to escrow each of these transactions and tie them to the revolution of a specific point lock / secret which then allows for settlement across each contract in lock step in the same way the HTLC contract works for escrow.

 
---

## Open Questions

### Volatility and Liquidations
Required to be baked into the contract and executed by the relevant wallet as a 50% price drop during a bond period (certainly not unheard of in a month long period), could potentially liquidiate the position on the long side requiring a pay out to the short position and establishment of a new bond for the short if they wish to remain in USD.

### Yield? 
Should there be a yield baked into the bond contract? Presumably this would be optional between parties, e.g. there is catastrophic loss risk for long side but not short, therefore you might expect the long sidde to expect some form of yield compensation for providing liquidity. 

### Price Feed Specs
More to come, my thinking here is to decentralise these across multiple exchanges or community groups. Might make more sense to fix the CYM to the USD as a more liquid market? 

### Contract Specs
Would need careful and standard spec for a good secondary market. 
Would need the ability to close at any point in time at the current price and settle back to sats. Perhaps these would be better as permentaly rolling 1 hour contracts…. 
Alternately the ability to swap out Alice for Charlie at the agreement of Alice and Bob. 

### The Clearnance Markets
Doesn't seem to me that this would only require a single market / match maker many markets may infact be prefereable or a peer to peer order book similar to bisq / joinmarket.
Current thinking is wondering if something like NOstr with lighteight easily hosted relays could solve htis problem whiulst also allowing for public key based reputation to be bootstrapped?
