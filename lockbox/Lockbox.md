# Lockbox Transaction Construction

#### An offchain construction for bitcoin contract enforcement

***Note*** This is provided as an unfinished high level concept seeking feedback!

The purpose of the lockbox contract contrsuction is to provide a set of pre-signed bitcoin transactions which can be reliably enforced in line with real world use cases.

It is assume this would be deployed over a channel factory construction in order to allow sufficient flexibility.  

More information on [channel factory construction is availabe in the whitepaper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6124062/).

The proposal is to have both pre-commit to a set of transactions which could be settled to the bitcoin blockchain which include both the payments as collatoral and an agreed bond.  

These outputs will ensure that money is correctly paid in line with the agreed terms at the agreed times.

As the bet concludes (based on blocktime) either party can broadcast a secret in order to cede the bet to the other party, allowing the other party to sign an output and claim the btc.

In the case in which parties disagree, at an agreed timelock a set of arbitration transactions (held with an oracle - more details later) can be broadcast which allow the Oracle to claim the bond  of the losing party and pay out the bet for the winning party.

In the case where this fails a third timelocked set of transactions will default to a fallback set of outputs e.g. return funds, donate to Tor/BTCPay etc.

The following diagram shows this flow.

```flowchart
st=>start: Bet Proposed:
e=>end: Bet Paid
Bond returned
e2=>end: Bet Paid
Bond Paid to Oracle
e3=>end: Money returned /
Donated to BTCPay

op0=>operation: Commit to 
all outputs
op1=>operation: Time Elapses
sub1=>subroutine: My Subroutine
cond=>condition: Was the bet 
settled amicably
op2=>operation: TimeLock 1 
Expires
cond2=>condition: Does arbiter 
know outcome 
op4=>operation: Pays outcome
& keeps bond
op5=>operation: Timelock 2 
expires
op6=>operation: Fallback transaction 
executed


io=>inputoutput: catch something...

st->op0->op1->cond
cond(yes)->e
cond(no)->op2->cond2
cond2(yes)->op4->e2
cond2(no)->op5->op6->e3
```

As we can be seen there are at least three actors required in order to execute this contract:

- **Party A:** Provides funds/bond, generates pre-images and pre-signs transactions.

- **Party B:** Provides funds/bond, generates pre-images and pre-signs transactions.

- **Oracle:** Service provider who holds a set of punishment transactions and can earn bond fees.

This closely mimics a real life "betting" arrangement in which a third party is selected to  hold funds in escrow and ensure the payout to the winner. However we incentivise the indivudal parties to gracefully concede the bet, as they will lose their bond if time elapses and the Oracle has to sign.

This is achieved by pre-agreeing to a set of transactions as shown below:

![Lockbox_1.png](Lockbox_1.png)

**Set 1: Happy Path**

This includes two pre-signed t(x). Which require a pre-image to be supplied to redeem the script.  The alternating party holds the pre-image required for redemption and as such can reveal this at any time allowing their counterparty to close out the bet successfully.

**Set 2: Enforcement Path**

This will again include two pre-signed t(x).  In this instance instead of returning the bonds to the original participants the bond of the losing party is instead paid to the Oracle broadcasting the transaction.

--- 

### But Pete - how does this actually happen?

Glad you asked...

As we covered in the article "Smart Contracts will be hired" what e're actually doing here is 

![Lockbox_2.png](Lockbox_2.png)

What if the Oracle can't know the outcome?
