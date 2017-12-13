
---
layout: post
title: What makes a chatbot great?
published: false
---

Last month I attended the Big Data London conference. One of the sessions run by Microsoft had a slide that roughly read like 


### What makes a bot great?

> - not how much "AI" it has
> - Not how sophisticated the language model is
> - Not whether it uses voice
> - Not whether it used guided UI

### It is the personality of the bot that makes it great

## What does "personality of a bot" even mean?
Honestly, it is as complicated as personality of us humans. There is no one way to define what a great personality is. It's a combination of a number of personality traits. And the same is true for bots. There are a number of traits that a great bot has. In this post, I will go over some of these traits that I have learned. 

## #1 - Give your bot some character
First of all, give your bot a name. When we built our first bot we did not do this. We ended up having everyone refer to it as just a chatbot. But then we learned that you can make the bot more lively simply by giving it a name. Now, when you are giving it a name, think about whether you want it to be male or a female character. 

Do you want your bot to come across as as a machine or as a human. This is very important and will go a long way in giving your bot a character. Generally, bots with machine-like characters will be mostly very static in their conversations where as human-like bots will engage their users with lively conversations. 

Once you have done that, think of a bot persona. A number of factors will drive the bot persona - demographics of the target customer base, business domain and the task at hand, to name a few. Bot persona will help you greatly when you are work out responses to different situations.  

## #2 - Be humorous
Humour is everywhere around us, so why not with bots? When we ran the first internal test of our bot, a significant proportion of conversations started with users trying to be humorous. Even when your bot is built around a non-humorous business problem, the moment users find out that they are talking to a bot, there will always be a few who would try to be naughty and start saying funny things to the bot. You may not want to go overboard with handling every possibility in the universe but having humorous responses to some funny statements from the users will make your bot stand out. 

## #3 - Do not be monotonous
This is the most important thing. Over time, your users will keep coming back to the bot and ask similar questions. It is easy to build a non-lively conversation by having the bot respond in a monotonous manner. 
Imagine you welcome every time the user starts talking to the bot. If you welcome the user by saying "Welcome back Bob" every time, then soon, that will become very monotonous and less engaging for the user. 

It does not take a lot to bring variation in bot responses if you are using tools like Watson Conversation or Microsoft Botframework. Most of us will ignore this during development as it's an overhead. But do not forget to add this in before you go live or even go out for a wider beta test. And do not add this just for the welcome message but for every response that is coming back from the bot. 

## #4 - Handle small talk
Small talk is relatively straight forward to handle and very easy to fall through the cracks. Some bot services like Dialog Flow will handle small talk automatically for you. All you have to do it enable it. But for others, you need to build conversations around small talk. If you are sailing in this boat, consider the following 

1. Greet the user with a welcome message at the beginning of the conversation and assume that user may reply with small talk like "thanks", "hello". 
2. Always end the conversation with small talk like "bye", "see you soon" etc. and assume that user will respond with similar words
3. Messaging is inherently slow and full of latency so it's possible that user become impatient when they do not see a response from the bot in time. Some user may try to talk to the bot using word like "Hi", "Still there?" while bot is still working on their previous request. It's best to handle such utterances appropriately. and make sure that you remove monotony from these responses. 

## #5 - Handle out of context conversations to a reasonable degree

## #6 - Offer a help menu

## #7 - Hand off to a human before the conversation becomes too frustrating for the user

## #8 - Use sentiment analysis tools to determine user's mood


