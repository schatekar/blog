---
layout: post
title: Random thoughts on load testing - Transaction Mix
excerpt: Transaction mix let's you mimic how the real users will use different features of your website. A right transaction mix let's us project the right website performance with the right server capacity needed.
tweet: Next time you run a load test, make sure you use the right transaction mix
published: true
---

This post is part of a series - [Random thoughts on load testing](http://chatekar.com/random-thoughts-on-load-testing/). 

Today we tak about __Transaction Mix__. 

## Transaction Mix

If you record all the user journeys in a tool like JMeter and then run them under load, you are missing a very important aspect called Transaction Mix. It let's you mimic how the real users will use different features of your website. 

Let's use a fictitious example to understand what a transaction mix is. Let's we have a very simple e-commerce website that we want to load test. About 100K users visit this website every day. About 30K users login. 2000 users add one or more items to their basket. Roughly 500 users successfully checkout. 

There are two things worth noticing here

1. Not all users are using all features of the website. Some users drop out before they add any product to basket. 
2. Not all users are using the same feature at any point. In other words, while some users are logging in, others are adding a product to their basket, while others are checking out. 

Your load test scenario will be most effective when it tries to mimic this end user behaviour. If we are running a load test for the above website using a very simple load pattern like below

1. Start with 100 concurrent virtual users
2. Add 10 new virtual user every 2 seconds for next 20 seconds

You will end up with a total of 200 virtual users at the end of your test. For your load test to match the real end-user behaviour, you have 

1. All the users hitting the home page of the website 
2. Roughly 60 users are logging in
3. Around 4 users adding a product to the basket
4. 1 user successfully checking out

There are possibly more nuances to this that I have ignored to keep the example simple. For instance, Of the 4 users who add one or more product to their basket, 3 users are logged in and one is using the website as a guest user. 

You may have noticed that if we did not use a proper transaction mix like above, then we would have ended up with one of the two things

1. We overload some of the features with unrealistic user base. If we are testing against a product-like setup to get an idea of website performance then we would be projecting a worse picture than how it is going to look like in reality
2. Or if we are doing this exercise to guess needed server capacity for a given load, then we would provision way more servers than we actually need.

A right transaction mix let's us project the right website performance with the right server capacity needed. 

## Working out the right transaction mix

So how do you find out what the right transaction mix is for your product? If you are load testing a new major version of an existing product, then this is actually very easy. You have a number of places where you can look for this information. The first place you should be looking at and your best bet would be website analytics. Website analytics will give you the most precise view of how user are using different website features. 

If you do not have website analytics setup or you are unable to get access this data, then your next best shot is application logs. The quality of this data would depend on how application logging is setup in your system sand what tools you are using to capture and store application logs. If you are using enterprise tools like [New Relic](https://newrelic.com/) or [Splunk](https://www.splunk.com/) then querying the application logs to find out how different parts of the applications are using is relatively straight-forward. Even with an open source tool set like [ELK](https://www.elastic.co/webinars/introduction-elk-stack) getting this data should be easy. You will have a real challenge if you are still writing application logs in a file on the server. In that case, you will have to rely on other data combined with some guess work. For example, you can query the database to find out how many new users are registering every day or how many people are logging in on daily basis. This will not give a complete picture but at least your guess work will be based on some real data. 

None of this will work if you are load testing a new application. In this case, your only option is guess work. But you can base the guess work on a solid foundation by using the numbers from business case. Most products are backed by a business case. When your product manager put together the business case, they would have given a serious thought to how the consumers are going to use their product. This would mostly be in the form of funnel analysis over a period of time. It can go something like this __Over a period of 18 months, we expect 100K users to visit our website, of which 50% would register for a free account and 5% will end up becoming paid customers.__ In my mind, these numbers are a more solid foundation for our guess work than querying application database.



