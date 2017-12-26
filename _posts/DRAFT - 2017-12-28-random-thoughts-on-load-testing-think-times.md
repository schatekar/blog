---
layout: post
title: Random thoughts on load testing - Think Times & User Profiles
excerpt: Think Times and User Profiles are another nice techniques that lets you mimic the end user behaviour in your load tests. Used correctly, these techniques will result in your test scenario following then expected load pattern leading to more reliable test results
published: false
---

This post is part of a series - [Random thoughts on load testing](http://chatekar.com/random-thoughts-on-load-testing/). 

Today we tak about __Think Times & User Profiles__. In the [previous post](http://chatekar.com/random-thoughts-on-load-testing-transaction-mix/) we talked about using transaction mix in order to mimic the actual end user behaviour in our load test. But you won't be truly mimicking the end user behaviour unless you use think times and user profiles. 

## Think Times
Real users do not go on loading one page after another incessantly. They take their time to look at the page content and then decide where they want to go next. If one of the pages needs the user to submit some information before they can go ahead, it takes some time for the user to key in the needed information. Look another way, some time passes between two page loads, always. This time is called __Think Time__ because the user is taking time to think (and read, submit data) before they go to the next page. Your load test should consider think times between successive requests that it sends to the server from the same virtual user. 

A returning user or a frequent visitor may not spend the same amount of time as a new user to go through the page content before they decide where to go next. This is where __User Profiles__ comes in.

## User Profiles
User profiles is a way to segment the users into different buckets depending on their behaviour. There is really not a hard and fast way to segment the users. You will need to use your instinct and data to segment the users. For example, if you have a login feature then two segments of users could be as follows

1. The users who use password manager to automatically fill in username/password information on the login page
2. The other set of users who manually enter username/password every time they want to login

This is one representative segmentation based on end-user behaviour that tells us that the think times for the login journey can be different for different set of users. Besides working out potential think times, user profiles can also be used to tweak the transaction mix to reflect true end user behaviour. 

## How to work out think times and user profiles?

## How to use think times and user profiles?


