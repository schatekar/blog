---
layout: post
title: Explain bitcoin like I am 5 year old
---

I have tried to explain how bitcoin works to a number of different people. With some I have been able to get to the low level detail like merkle trees but with others, I have failed miserably to continue the conversation beyond 5 minutes. I recently had a eureka moment of the __dumbest ever explanation of bitcoin__. I will leave it to the readers to tell me if has worked. So let's get started

## 1) A room-full of people

Imagine a room with a big round table in the middle and a number of people sitting around that table. Each person has a piece of paper in their hand. This paper lists how much money every person in the room holds. But this information is not written as plain number. Instead, it is written like below

|Person|Unspent Transactions|
|------|--------------------|
| Alice | [1] -> $50 |
| Bob   | [2] -> $30 |

What does that mean? It means, at some point in past, someone had transferred $50 to Alice that she as not spend yet. Meaning, Alice has $50 that she can spend. Similarly, Bob has $30 that he can spend. 

### Removing the dumb lense

- The room is the bitcoin network. 
- Each person in the room is a node in the bitcoin network. The piece of paper that each person has is a block in the [blockchain](https://bitcoin.org/en/developer-guide#block-chain) (the distributed ledger that underpins bitcoin). 
- Each person is [public kay](https://bitcoin.org/en/glossary/private-key) 
- Each unspent transaction is [UTXO](https://bitcoin.org/en/glossary/unspent-transaction-output)


## 2) Alice wants to transfer money to Bob

Let's say Alice wants to transfer $30 to Bob. In order to do that, Alice will announce to the room that she is going to be spending $30 from the transaction that has not spent yet. This is the `[1] -> $50` transaction against Alice's name. Now, everyone in the room listens to that and they all check on their paper if Alice has an unspent transaction that allows her to transfer $30 to Bob. In this case, Alice has such a transaction so everyone in the room approvers her transfer of $30 to Bob.

> It is worth highlighting that people in the room do not ask each other if they should approve Alice's transaction. They all just check on their own piece of paper if Alice has the transaction in her name she is claiming to transfer money out of. This is how bitcoin removes the need for a trusted third party that approves every transaction. 

"What does that mean?" you may ask. After all, we need a proper trail of how money is being transferred from one person to another. Here is what happen next. Everyone in the room has two more pieces of paper. 

### 2.1) The first piece of paper

Let's call this paper __transaction log__. This is where everyone makes a note of the transaction that was just approved. The exact details of this gets recorded is not important, but for the sake of conversation, let's say, it's recorded as `[1] -> Alice to Bob, $30 -> [4], [5], 23456957`. Here, `[1]` is the input transaction from the previous piece of paper from where the money required for this transaction was sourced. What are `[4]`, `[5]` and `23456957`? Let's look at second piece of paper to understand what are they. 

### 2.2) The second piece of paper

Let's call this paper __unspent transaction log__. This is where transactions that are still not spent are maintained. This is where bitcoin becomes a bit tricky. So read the next paragraph twice if you have to. 

When we started, Alice had $50 and Bob had $30. Alice transferred $30 to Bob. So effectively Alice is left with $20 and Bob has $60 in total. In bitcoin system, we always maintain the balance that everyone holds in the form of a number of unspent transactions. If you think of Alice's recent transaction this way, you will notice that, Alice is now left with an unspent transaction of $20. This is the `[5]` that we introduced in the previous paragraph. In the same way, Bob has a new unspent transaction of $30 that he just received from Alice. This is the `[4]` in the previous paragraph. At this point, everyone in the room, make the following two entries on this second piece of paper that they have

|Person|Unspent Transactions|
|------|--------------------|
| Alice | [5] -> $20 |
| Bob   | [4] -> $30 |

If you have noticed, this looks exactly same as the very first piece of paper that everyone in the room started with. If you are thinking that everyone started with __unspent transaction log__ then you would be right. 

### 2.3) What about 23456957?

This is just a random number that everyone comes up with together and is written next to the transaction. It has a purpose which will become clear shortly. 

So at this point, we have these three piece of paper that everyone in the room has. 

XXXXXXXXxx

## 3) Bob wants to transfer money to Alice

Anyone can announce that they want to transfer money just like Alice did. Everyone goes through the same steps every time someone in the room wants to transfer money to someone. 


