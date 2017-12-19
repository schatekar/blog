---
layout: post
title: Bitcoin Pub Analogy
published: false
---
Non-technical people find it difficult to understand how bitcoin (and consequently the blockchain) works. One of the reasons for this could be that the most explanations on the internet either take away a lot of important technical details or keep a lot of details in. Both results in confusion. Complex topics like bitcoin and blockchain can best be explained by using an everyday analogy. So here is one for you. But before we go into the analogy, let's spend a few moments understanding how payments work. 

## Payments in a world without blockchain
When you pay at a shop using your card or transfer money to your friend's bank account, among a lot of other details, there is one important thing happening. Your bank and the other party's bank (the shop owner or your friend) are ensuring that the transaction is valid and can go through. In this scenario, you are trusting your bank to make sure that every transaction is valid. The bank is the trusted third party without which transactions like these cannot happen. 

In bitcoin/blockchain world, there is no trusted third party. Then who ensures that only valid transactions go through? Though, there is no trusted third party in bitcoin, there is trust and that trust is distributed among every participant of bitcoin. Every participant plays by the rules making the distributed trust difficult to break. I have a pub analogy for you to understand how this distributed trust works.  

## A huge crowded pub
All of us have been to a pub. We know how it is, specifically on a Friday evening. A lot of people crammed into a big room, a lot of noise but you can barely hear the person next to you. But you still only talk to the person next to you. A bitcoin network is exactly like that. 

For our analogy to work, let's make some assumptions

1. The pub takes payments in a crypto-currency called the pubcoin (Just a fancy name to keep up with the analogy)
2. There is no bartender who can take payments
3. The pub relies on their customers to ensure that every payment that customers make is valid

Let's also assume that everyone has 50 pubcoins, to begin with.<sup>1<sup>

Everyone in the pub has a piece of paper that lists how many pubcoins everyone in the pub has.<sup>2</sup> Let's call this piece of paper __balance sheet__.

## Bob wants to pay for his beer
Bob, our friend at the pub, wants to pay for his beer. Bob does what he can do in a pub like this. He tells people standing next to him, that he would like to transfer 5 pubcoins to the bartender. Those people check on their balance sheet if Bob really has 5 pubcoins to make that transaction. In this case, because Bob has 50 pubcoins, these people are going to assume that this is a valid transaction. These people then tell the other people next to them that Bob wants to transfer 5 pubcoins to the bartender. And those people follow the suit. Eventually, everyone in the pub knows that bob is transferring 5 pubcoins to the bartender. 

> If Bob did not have enough pubcoins required to make that transaction, then the people next to him, who he told about the transaction, would not have propagated the transaction to the rest of the people in the pub. This is how invalid transfers get rejected without a need for a trusted third party

Anyone in the pub can pay the bartender or transfer pubcoins to others in the pub using the same mechanic. 

## What stops Bob from spending more than what he has
Let's say Bob is not a genuine guy we thought he is. Bob notices that it takes a certain amount of time for his transfer message to reach every other person in the pub. So he sees an opportunity to spend more pubcoins than he has. 

After he tells a couple of people that he wants to transfer 5 pubcoins to the bartender. He quickly moves to a different group of people and tells them that he would like to transfer 50 pubcoins to one his friends. Now, these people have not received Bob's previous transaction of 5 pubcoins so they think it's valid for Bob to make this transfer of 50 pubcoins. So they start spreading around this transaction. 

__Has Bob managed to fool the system?__

He would have if it was not for another mechanism that helps everyone in the pub to verify that a transaction is not a double-spend. 

## Walls with indelible list of confirmed transactions
There is a person by every wall of the pub. They have a special job for which they get rewarded<sup>3<sup>. As every transaction passes through them, they write it down on another piece of paper. In addition to ensuring that every transaction is valid, they also ensure that no transaction is resulting in double-spend. And if it does, they just reject the transaction causing double-spend. In case of Bob, one of his two transactions will be rejected by the people manning the walls. Whichever transaction is received first, will be kept as valid transaction (given it passes all the checks). It is possible that some of people by the wall reject the 5 pubcoins transactions while others reject the 50 pubcoins transaction. It all depends on who got which transaction first. I know this is confusing but just carry on for next few paragraphs and it will become clearer.  

These people have a way to talk to each other. Every 10 minutes, they choose one of them to be the leader of the group of people manning the walls. This leader, writes every valid transaction that they have known about in the last 10 minutes on the wall. It is written in a way that it is visible to everyone in the pub and cannot be erased by anyone. People manning the other walls see these new transactions on the wall and they write the exact same transactions on their wall for everyone else to see. These set of transactions are called a block. 

If the leader had confirmed the 5 pubcoin transaction that Bob initiated, then that is the transaction that gets reflected on all the walls. The other transaction for 50 pubcoins just disappears. 

## Time to refresh the balances or throw their pint glasses at the wall
When the new confirmed transactions get put up on the wall every 10 minutes, everyone in the pub take a note of every transaction. They run the validation checks again on every transaction. If all the transactions are valid, they update their own copy of balance sheet based on those transactions. In this instance, everyone will change Bob's balance from 50 pubcoins to 45 pubcoins in their own copies. Next time Bob wants to pay someone, everyone knows that Bob is left with 45 pubcoins.  

If any of the transaction on the wall is not valid, everyone throws their pint glass at the wall until the person takes down all those transactions from the wall. If this happens, other people manning the wall, also take down the transactions that they had copied from this wall,  a new leader is chosen, and it's the responsibility of the new leader to reflect the new block of transactions on the wall. 

What do you think? Has this analogy helped you understand how bitcoin works? Welcome any feedback that will improve this article. 

### Footnotes
1. In the real bitcoin world, people just do not end up with some bitcoins, they either get them from other people holding them or they mine them. But let's not make our analogy any more complicated just yet
2. Again, in the real bitcoin world, this list is made up of something called [Unspent Transaction Output](https://bitcoin.org/en/glossary/unspent-transaction-output) but let's keep things simple for the purpose of this analogy
3. These are called miners in the bitcoin world. Their job is to put together the next block in the chain and confirm the transactions that should go in that block. You may know that they do get rewarded for their work. 