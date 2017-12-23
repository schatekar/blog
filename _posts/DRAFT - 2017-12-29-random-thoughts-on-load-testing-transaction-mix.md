---
layout: post
title: Random thoughts on load testing - Transaction Mix
excerpt: 
published: false
---


## Transaction Mix

Let's say you are testing a very simple event ticket booking website. A user would either register and then login or login directly using one of the supported social login methods. After logging in, they search for events near them, read various details and once they make up their minds, they head to checkout. The checkout in itself is a multi-step process. 

If you record all the user journeys in a tool like JMeter and then run them under load, you are missing a very important aspect called Transaction Mix. Transaction mix let's you mimic how the real users will use different features of your website. If you are expecting 100K users to visit your website everyday, them may be 50% of them login. Of those 100K people hitting your website, almost everyone will search for events and browse different pages until roughly 10% of them decide to checkout. In the end, only 1% successfully checkout. 

> I have made up all those numbers. You would have a better idea of how those numbers stack up for your website.

There are two things worth noticing here

1. Not all users are using all features of the product
2. Not all users are using the same feature at any point

Your load test scenario will be most effective when it tries to mimic this end user behaviour. Looking at the example from the previous paragraph again, we can say that

1. 100% of the users are searching for event and browing  through the details of the events
2. 50% of the users are logging in 
3. 10% of the users are intiating the checkout flow
4. 1% of the users are finishing the checkout

It will be wrong if our load test scenario  had every user finshing the checkout. We will be testing for 100 times more load than what we are expecting to have. If the load testing exercise was performed for server sizing, then we would end up with over-sizing the required capacity. If the purpose waa to determine the response times, then we would paint a worse picture then what we could see in proeuction. 

## Working out the right transaction mix





