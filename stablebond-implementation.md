# Example Implementation for Stablebonds

Stablebonds referred to as bUSD represent a fixed amount of USD exposure, created as a synthetic instrument betweeb two peers in a discrete log contract. This is achievable now, however, there are several design considerations when looking to scale this to more people and create a tradable (i.e. for products and services) curency.

## Creation of Stable Bonds
Instead of the traditional approach of issuing bearer tokens representing bUSD we instead enter into a short term bond contract which is denominated in USD and collateralised on both sides by BTC. 

This allows any individual or organisation to “mint" bUSD by entering a DLC contract in a peer to peer contract which goes short bitcoin against USD over a 4320 block (1 month) or 144 block (1 day) period.

This person now has an stable balance which can be displayed in a wallet application for ease of use. At the end of the period this will settle back into bitcoin.  Should the user want retain a USD balance they would roll forward the bond. 

This of course requires a liquid market for bUSD offers, or put another way this requires there to be a liquid market of people who want to go levered long bitcoin :).



## 

At any time, this person could agree with their counterpart to “roll” this contract forward (this is a 2-of-2 multis so can be collaboratively closed and reopened) or failing that the contract settles and they can simple open up another contract to maintain their CYM balance, indeed the wallet could be instructed to do this automatically.
 
Ideally this contract would also have a "closeing term" which setles the contract at that time with a small fee paid to the "maker".

Let’s wave our magic wand and assume we fund and settle these contracts on lightning.

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
