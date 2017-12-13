---
layout: post
title: Bitcoin Pub Analogy
published: false
---
I have tried to explain how Bitcoin works to a number of different people. With some, I have been able to get to the low-level detail like Merkle trees but with others, I have failed miserably to continue the conversation beyond 5 minutes. I recently had a eureka moment of the __best real life analogy for bitcoin__. I will leave it to the readers to tell me if it has worked. So let's get started


## A huge crowded pub
All of us have been to a pub. We know how it is, specifically on a Friday evening. A lot of people crammed into a big room, a lot of noise but you can barely hear the person next to you. But you still only talk to the person next to you. A bitcoin network is exactly like that. 

For our analogy to work, let's make some assumptions

1. The pub takes payments in a crypto-currency called the pubcoin
2. There is no bartender who can take payments
3. The pub relies on their customers to ensure that every payment that customers make is valid

Let's also assume that everyone has 50 pubcoins, to begin with.<sup>1<sup>

Everyone in the pub has a piece of paper that lists how many pubcoins everyone in the pub has.<sup>2</sup> Let's call this piece of paper __balance sheet__ (only because it's easy to remember)

## Bob wants to pay for his beer
Bob, our friend at the pub, wants to pay for his beer. Bob does what he can do in a pub like this. He tells people standing next to him, that he would like to transfer 5 pubcoins to the bartender. Those people check on their balance sheet if Bob really has 5 pubcoins to make that transaction. In this case, because Bob has 50 pubcoins, these people are going to assume that this is a valid transaction. Next, these people will tell the other people next to them that Bob wants to transfer 5 pubcoins to the bartender. And those people follow the same thing. Eventually, everyone in the pub knows that bob is transferring 5 pubcoins to the bartender. 

> If Bob did not have enough pubcoins required to make that transaction, then the people next to him, who he told about the transaction, would not have propagated the transaction to the rest of the people in the pub. This is how invalid transfers get rejected (or in other words, do not make it to everyone's copy of the balance sheet) without a need for a trusted third party 

Anyone in the pub can pay the bartender or transfer pubcoins to others in the pub using the same mechanic. Once the message to transfer has propagated to everyone in the pub, everyone's balance sheet would be updated to reflect the latest balances. Taking the above example forward, when Bob's message is propagated to everyone in the pub, the balance sheets would reflect that Bob is now left with 45 pubcoins and bartender now has 5 more pubcoins than what she had before. 

## What stops Bob from spending more than what he has
Let's say Bob is not a genuine guy we thought he is. Bob notices that it takes a certain amount of time for his transfer message to reach every other person in the pub. So he sees an opportunity to spend more pubcoins than he has. 

After he tells a couple of people that he wants to transfer 5 pubcoins to the bartender. He quickly moves to a different group of people and tells them that he would like to transfer 50 pubcoins to one his friends. Now, these people have not received Bob's previous transaction of 5 pubcoins so they think it's valid for Bob to make this transfer of 50 pubcoins. So they start spreading around this transaction. 

__Has Bob managed to fool the system?__

He would have if it was not for another set of validations and a cool trick that stops Bob from sending the second transfer. 

## Two types of people
There are actually two types of people in the pub

1. __Type A__ people, who perform validations on the transactions and if valid, pass the message on to next people 
2. __Type B__ people, who do the above but also keep a log of every message they forwarded on another piece of paper 

Let's call this second piece of paper a __Transaction Log__ (Remember, everyone already has a piece of paper called __Balance Sheet__). The type B people, who are recording every transfer on transaction log, are also doing one more thing.<sup>3</sup> They are building a lock and key to a transparent box. Only one of them is going to be able to build this lock and key as the lock has to match a specific description (size, colour, weight etc.). This description keeps changing every now and then. Once someone manages to come up with a right lock and key, they follow that with the below

1. They take a guess at number of people in the pub
2. They come up with that number of copies of the lock and key
3. The create that same number of copies of the transaction log
4. They keep the transaction log in the box in such a way that anyone having a box can read the transactions on there
5. They start distributing the box other people in the pub

Every person that receives the box verifies that the lock satisfies the condition in effect at that point in time. If not, they throw the box away. 

## How does this stop Bob from spending the money he does not have?

This is where the additional set of validations come into the picture. The type B people do not accept two transactions coming from the same person. They discard the second one. But this leads to a more complicated situation. There would some type B people who would receive the 5 pubcoin transfer first and discard the 50 pubcoin transfer. There would be other type B people who would do exactly opposite and discard the 5 pubcoin transfer. That is a problem, isn't it? Well, the good news is - when one comes up with the lock for that transparent box, everyone gets a copy of that box. At this point, all type B people drop their transaction log and refer to the one in the box. So eventually, everyone in the pub gets a copy of the transaction log that lists only one of the two transactions that Bob did.

A new box is built every fixed amount of time i.e. every 10 minutes in case of bitcoin. While the box is being built, Bob can only make a single transfer of the amount that he has.<sup>4</sup>

## What about the balance sheets that everyone is holding?
We have another friend in the pub, Jack, who received the message about Bob transferring 50 pubcoins to his friend. So Jack updated his balance sheet to say Bob does not have any pubcoins left. But when he received the transparent box, he noticed that Bob's transfer of 50 pubcoins never went through. Now Jack is left with a wrong balance sheet. 

When everyone receives a copy of the transparent box, they are supposed to go through every transaction in the box and update their balance sheet appropriately. Rather, it is at this point that everyone updates their balance sheet and not when they had received a transfer message from their neighbour. This way, everyone, always has the correct balance sheet. 

## What stops Bob from creating a box himself with fake transactions?
On the face of it, it seems possible for Bob to keep handing out a box that he himself put together with some fake transactions in it. But when this box is handed out to every other person in the pub, they do not just blindly accept the box. They ensure that every transaction in the box is a valid transaction. So Bob's invalid transaction cannot go much further. 

## Relating back to bitcoin

This analogy is of no use if I could not tie it back to the real Bitcoin network. So let me draw parallels between the two

1. The pub is bitcoin network
2. Every person in the pub is a bitcoin node
3. Type A people are full nodes (There are also lightweight nodes that I completely skipped in this analogy)
4. Type B people are mining nodes
5. Balance sheet is UTXO database
6. Transaction log is blockchain (Not entirely but close)
7. Transparent box is a block in the blockchain (a block contains all the confirmed transactions)
8. Lock and key is analogous to hash of block
9. Coming up with a lock and key matching exact specification is proof of work

If you have never looked under the bonnet of bitcoin/blockchain, feel free to ignore these parallels. 

What do you think? Has this analogy helped you understand how bitcoin works? Welcome any feedback that will improve this article. 

### Footnotes
1. In the real bitcoin world, people just do not end up with some bitcoins, they either get them from other people holding them or they mine them. But let's not make our analogy any more complicated just yet
2. Again, in the real bitcoin world, this list is made up of something called [Unspent Transaction Output](https://bitcoin.org/en/glossary/unspent-transaction-output) but let's keep things simple for the purpose of this analogy
3. This is where the analogy seems far-fetched but this is the best analogy I have managed to come up with for something that is so complex
4. In reality, Bob can make more than one transfers owing to how balance sheets are written but I am going to keep this simple here