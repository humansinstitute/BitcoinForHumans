# Stable Bonds

## An approach to community based bitcoin backed stable currencies (like a stablecoin but not)

An alternative idea for creation of stable coins.  The core concept is that instead of utilising a “bearer token” backed by collateral (in a bank or a smart contract) we utilises markets and long / short preference to manage stability.  

The mental model I choose to think about this is to consider stable bonds as a bitcon collateralised bond market.  

Whats more we believe we can create this in a trust minimised peer to peer architectire.   

*(This is very much a draft and there are a lot of edge cases to talk through I think, but the basic concepts and I would welcome discussion - Pete)*

---

## Overview

## Possible Implementation Pattern

[[stablebond-implementation.md]] 
 
---

## Open Questions

### Price Feed Specs
More to come, my thinking here is to decentralise these across multiple exchanges or community groups. Might make more sense to fix the CYM to the USD as a more liquid market? 

### Contract Specs
Would need careful and standard spec for a good secondary market. 
Would need the ability to close at any point in time at the current price and settle back to sats. Perhaps these would be better as permentaly rolling 1 hour contracts…. 
Alternately the ability to swap out Alice for Charlie at the agreement of Alice and Bob. 

### The Clearnance Markets
Doesn't seem to me that this would only require a single market / match maker many markets may infact be prefereable or a peer to peer order book similar to bisq / joinmarket.
Current thinking is wondering if something like NOstr with lighteight easily hosted relays could solve htis problem whiulst also allowing for public key based reputation to be bootstrapped?
