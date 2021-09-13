# Stable Bonds

## An approach to community based bitcoin backed stable currencies (like a stable coin but not)

*This should be read as an exploration of an alternative approach for the creation of stable coins, or in this instance non-coin but stable value.  Please be aware this is a work in progress to flesh out and test an idea.*

The core concept of Stable Bonds is that instead of utilizing a “bearer token” backed by collateral (in a bank or a smart contract) we utilizes markets and long / short preference to manage stability through peer to peer contracts.

In effect we create a market driven alternative model of the "auto-dollar-conversion" mechanism which has been proposed in El Salvador. 

Were a deep liquid market to develop to offer this service on native bitcoin rails, we could onboard people directly to bitcoin the network, without the volatility inherent in bitcoin the asset. 

I believe it is reasonable assertion in a trust minimized private market, which allows users to hold dollar denominated value without counter party risk. 
 
This would allow any individual or institution (for example a community bank which wanted to offer USD denominated accounts on bitcoin native rails - e.g. offshore in Africa, South America) to elect to store a percentage of their bitcoin wealth in a "stable" form (defined as approximately pegged to the market exchange price of BTC/USD).  

This capability could then reduce the volatility and risk inherent in the earning and storing BTC when living in a hand to mouth fashion. I believe this in turn would allow easier adoption of bitcoin, where it is most needed, if individuals could earn "USD on native bitcoin rails" and then engage in native swaps to bitcoin, where they please, to facilitate long term savings.

If a user were holding stablebonds and wanted to perform a transaction the users wallet would in real time settle the bond contract into the market and transact over lightning. If the merchant wanted to receive this in lightning, no further action is necessary. If however, they prefer dollar value, they can simply purchase a bond on the market. 

No tokens, all bitcoin collateralized channels.

![Community Bank Flow](https://raw.githubusercontent.com/humansinstitute/BitcoinForHumans/master/assets/stablebond-flow.gif)

![Community Bank Flow - Animated higher res](https://raw.githubusercontent.com/humansinstitute/BitcoinForHumans/master/assets/stable-bond-flow.mp4)

An example payment flow for a community bank and animated mp4 version. 

The name "stablebonds" was chosen as no coins were created and I was seeking some differentiation. Although I appreciate this isn't so much a bond in any true sense, however, this does act more in line with a peer to peer repo-market which generates cash from collateral and has potnetial for a yield curve on difference length contracts so it kinda fits. It's also a cheeky nod to the fact that nothing in bitcoin is really named properly (wallets, coins etc).

*(This is very much a draft and there are a lot of edge cases to talk through I think, but the basic concepts and I would welcome discussion - Pete)*

---

## Overview

![Community Bank Flow](https://raw.githubusercontent.com/humansinstitute/BitcoinForHumans/master/assets/stablebond-flow.jpg)

The proposed stack would require several logical components. 

* [[Stablebond-Wallet]]: This is the app layer which integrates with lightning and bitcoin nodes, handles communication in the market and negoatiates bUSD Swaps and manages payments and settlement of contracts. It would ideally be implemented as a library and included in existing applciation stacks, for example integration into Sphinx.Chat would allow the applicaiton to inherit existing groups, identity and reputation information.
* [[Stable Bond Contract Format]]: This describes a standard contract and protocol for creating 1 day and 1 month bonds. Standardization of the contract, and potentially set amounts, would encourage routing of bond contracts as a means of creating liquid secondary markets and optionality for "coinage" e.g 1 / 5 / 10 dollar notes.  
* [[Stable Bond Exchange Market]]: This is a virtual market place which matches market makers willing to take the long or short side of individuals seeking stability of long exposure. It is likely that multiple markets may segregate and emerge based on supported functionality and localities (e.g. Wallets in Nigeria working without KYC for un-banked population versus US based regulated wallets with full KYC for merchants).
* [[BTCUSD Price Oracles]]: Any number of price Oracles could provide signed pricing messages in order to inform the DLC contract. 
* Bitcoin / Lightnin Wallet: To facilitate the payment and receipt of payments over lightning. 

Stablebonds (bUSD) represent a fixed amount of USD exposure.  These are created by each user as required as a synthetic instrument between two peers in a discrete log contract. This is technically feasible now and contracts have already been executed on bitcoins main chain which have settled a [stable dollar value bet with zero knowledge to the Oracle](https://suredbits.com/settlement-of-first-multi-oracle-dlc/). 

Whilst this is achievable now, however, there are several design considerations when looking to scale this to more people and create a tradeable (i.e. for products and services) currency, which I will continue to expand on as this design develops.

### Whos who

We have three core Personas interfacing in the stable bond system:

* **Sally Short:** Primarily Sally wants to retain USD spending power but would prefer (or has) to do this in a non-custodial way on bitcoin network rails.
*  **Larry Long:** Larry has bitcoin and is seeking to take leveraged long exposure to the bitcoin price in a non-custodial fashion. 
*  **Mikey Marky Maker:** Is an entrepreneur with a bitcoin balance of bitcoin and is seeking ways to put this to work in order to drive a yield. who will switch between the roles of Sally and Larry in order to provide liquidity both long and short in return for a yield paid by contract takers in the market. 
*  **Nelly Nonbank:** Nelly isn't a bank, but she is interested in providing "bank like services" in her community. She can't open a central bank account, but believes bitcoin rails could allow her to do this without permission (and she's right - f!ck yeah). 

The purpose of this design is to facilitate a number of use cases such as: 

* UC001: Sally has no bank account but would like to sell goods / services and receive $USD (or equivalent) to her phone. 
* UC002: Sally would like to hold USD securely outside of a bank account. 
* UC003: Sally would like to be able to create and hold bitcoin in a savings account under her control without a bank.
* UC004: Larry would like to go even more long Bitcoin without a counter party.    
* UC005: (Auntie) Nelly would like to create USD denominated bank accounts for her family and friends as her local currency is collapsing and luckily she has some bitcoin. 
* UC006: Mikey would like to make yield on his bitcoin by making a market in stable bonds in return for yield.
* UC007: Nelly's oportunistic cousin Welly, is interested in replicating Nellys services at a reduced fee (so she does because this is a free market).  

Each of these use cases will be explored in more detail as we go. For the most part the actions taken are commons across multiple personas, albeit the intentions and incentives differ, which will be interesting to explore. 

### Stable Bond Life Cycle

#### Stable Bond Market

The idea here is that if we can find peers that want to go long, then we can take the alternaitve side of the that trade. 

The purpose of the market is to provide a place for these two parties to meet. In our example above we reference both a "community bank" and "many providers". The point here is that ther can be many actors in this market as it is natively trustless in concept. The concept of a bank with many customers, simplifies this concept in implementation for the early phases (this "Bank" could however be as simple as a single person with the required liquidity running the banking functions).  

In a simple form you could imagine this as a simple "group chat app" which lets you post maker offers for new bonds terms - here standardization of the contract terms makes the negotiation simpler and the market more liquid. It would also be reasonable to expect this to diverge into multiple local markets based around local banking services nad lightning providers. 

Given the risk of draw down, it is suggested that these terms should be short and the parties should roll the contracts frequently. For example go short bitcoin for 144 blocks (1 day) paying a yield to maker of XY basis point to incentivise market makers to take the other side of the trade. 

Differnet trust models and from centralized actors to peer to peer could be utilised in the market.

What this really allows is for people to enter and leave bUSD contracts at will, assuming there is a liquid BTC/bUSD market.

The liquidity of the market will be driven by to desires (1) to hold stable dolar value outside the banking system and (2) the desire toe go leveraged long bitcoin in a trust minised non custodial fashion. 

History tells us we're probably on safe ground. 

#### Entering a stable bonds position

Instead of the traditional approach of issuing bearer tokens representing bUSD we instead enter into a short term 'bond' contract at the user level which is denominated in USD with BTC as the collateral on both sides to fund the contract. 

This allows any individual or organization to “mint" there own bUSD as required by entering a DLC contract in a peer to peer contract which goes short bitcoin against USD over a 4320 block (1 month) or 144 block (1 day) period.

Once established at any point in time this contract is worth a variable amount of sats, representing the dollar value referenced by the price feed. 

This person now has an stable balance which can be displayed in a wallet application for ease of use. At the end of the period this will settle back into bitcoin.  Should the user want retain a USD balance they would roll forward the bond. 

#### Exiting from the Stable Bond

At any time, this person could agree with their counter party to “roll” this contract forward (this is a 2-of-2 multisig so can be collaboratively closed and reopened - or "same again tomorrow").  

Failing that the contracts could be settled and they can simply open up another contract to maintain their bUSD balance, indeed the wallet could be instructed to do this automatically.
 
Ideally the contract would also have a "closing term" which would allow the contract at that time with a small fee paid to the counter party as agreed on up-front.

Let’s wave our magic wand and assume we fund and settle these contracts on lightning (TBD! Plent to do here). [HOLD] - Flesh this out. 

#### Transacting on bUSD

The spending can leverage lightning as the settlement layer. In reality this is a slightly more decentralized version of the model deployed by Strike. Which means our erstwhile user actually just obtains unencumbered bitcoin on lightning and doesn't worry himself to much about what currency the merchant is most interested in! 

1. Payer has synthetic exposure to USD
2. Payer trades out of synthetic position and into bitcoin on lightning
3. Payer pays in lightning with instant physical settlement
4.  Merchant receives lightning; -> optional defendant on preferences ;
5.  Merchant converts bitcoin to synthetic bUSD exposure ;) 

This can be considered by considering the “spending transaction” not from the point of view of a sat moving through the network but as a particular set of outputs post transaction.

Example:

* Start Alice has 10 bUSD, Bob has 0 bUSD.
* MAGIC HAPPENS
* END Alice has 5 bUSD, Bob has 5 bUSD. 

The trick is how to perform the magic and not tell the user about what happened. 

If each bUSD were an individual “token” Alice would simply give Bob five bUSD and we get the outcome. But there are other ways to achieve this outcome. 

Specifically the “MAGIC HAPPENS” could be one of a few different flows, which all arrive at the same conclusion if we assume a liquid market in stable bonds. Here we will assume Alice is paying Bob:

**Option 1** 
* Bob is selling in bUSD and wants to receive bUSD
* Bob is present and identifiable in the secondary market
* Alice takes her 10 bUSD contract to the secondary market and routes 5 bUSD of exposure to Bob.

**Option 2**
* Bob wants to sell in bUSD but receive in Sats. 
* Alice settles her 10 bUSD contract and routes the Sats to Bob.
* Alice buys a 5 bUSD contract from the market. 

**Option 3**
* As 2, but Bob wants to receive bUSD, but is not visible to Alice in the market. 
* Alice settles her 10 bUSD contract and routes the Sats to Bob.
* Alice buys a 5 bUSD contract from the market. 
* Bob buys a 5 bUSD contract from the market with his new Sats.

It should also be noted that community banks could step in to provide a service here (and this would be a great business model) to provide more liquidity to bond sales and remove the requirement to settle contracts overnight. 

For example if i were a bank with $1m of bitcoin collateral and I needed to maintain working cash of $100k over a 1 day period instead of settling my bUSD contracts at the point of sale I could simply open new contracts that net out my exposure in the opposite direction and wait for the bonds to settle after the allotted block time.  

[HOLD] It would be interesting to explore account based systems such as LN bits here and see how Uncle Jim, Aunti Nelly banks could be provisioned with multiple users.
 
---

## Open Questions

### Volatility Risk and Liquidations
Required to be baked into the contract and executed by the relevant wallet as a 50% price drop during a bond period (certainly not unheard of in a month long period), could potentially liquidiate the position on the long side requiring a pay out to the short position and establishment of a new bond for the short if they wish to remain in USD.

### Yield? 
Should there be a yield baked into the bond contract? Presumably this would be optional between parties, e.g. there is catastrophic loss risk for long side but not short, therefore you might expect the long sidde to expect some form of yield compensation for providing liquidity. 

### Routing of Contracts on Lightning

### The Role of Community Banks

### The Role of Market Makers

### Price Feed Specs
More to come, my thinking here is to decentralise these across multiple exchanges or community groups. Might make more sense to fix the CYM to the USD as a more liquid market? 

### Contract Specs
Would need careful and standard spec for a good secondary market. 
Would need the ability to close at any point in time at the current price and settle back to sats. Perhaps these would be better as permentaly rolling 1 hour contracts…. 
Alternately the ability to swap out Alice for Charlie at the agreement of Alice and Bob. 

### The Clearnance Markets
Doesn't seem to me that this would only require a single market / match maker many markets may infact be prefereable or a peer to peer order book similar to bisq / joinmarket.
Current thinking is wondering if something like NOstr with lighteight easily hosted relays could solve htis problem whiulst also allowing for public key based reputation to be bootstrapped?
