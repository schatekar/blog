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
Honestly, it is as complicated as the personality of us humans. There is no one way to define what a great personality is. It's a combination of a number of personality traits. And the same is true for bots. There are a number of traits that a great bot has. In this post, I will go over some of these traits that I have learned. 

## #1 - Give your bot some character
First of all, give your bot a name. When we built our first bot we did not do this. We ended up having everyone refer to it as just a chatbot. But then we learned that you can make the bot more lively simply by giving it a name. Now, when you are giving it a name, think about whether you want it to be male or a female character. 

Do you want your bot to come across as a machine or as a human. This is very important and will go a long way in giving your bot a character. Generally, bots with machine-like characters will be mostly very static in their conversations. On the other hand human-like bots will engage their users with lively conversations. 

Once you have done that, think of a bot persona. A number of factors will drive the bot persona - demographics of the target customer base, business domain and the task at hand, to name a few. Bot persona will help you greatly when you are work out responses to different situations.  

## #2 - Be humorous
Humour is everywhere around us, so why not with bots? When we ran the first internal test of our bot, a significant proportion of conversations started with users trying to be humorous. Even when your bot is built around a non-humorous business problem, the moment users find out that they are talking to a bot, there will always be a few who would try to be naughty and start saying funny things to the bot. You may not want to go overboard with handling every possibility in the universe but having humorous responses to some funny statements from the users will make your bot stand out. 

## #3 - Do not be monotonous
This is the most important thing. Over time, your users will keep coming back to the bot and ask similar questions. It is easy to build a non-lively conversation by having the bot respond in a monotonous manner. 
Imagine you welcome every time the user starts talking to the bot. If you welcome the user by saying "Welcome back Bob" every time, then soon, that will become very monotonous and less engaging for the user. 

It does not take a lot to bring variation in bot responses if you are using tools like Watson Conversation or Microsoft Bot framework. Most of us will ignore this during development as it's an overhead. But do not forget to add this in before you go live or even go out for a wider beta test. And do not add variations just for the welcome message but for every response that is coming back from the bot. 

## #4 - Handle small talk
Small talk is relatively straightforward to handle and very easy to fall through the cracks. Some bot services like Dialog Flow will handle small talk automatically for you. All you have to do it enable it. But for others, you need to build conversations around small talk. If you are sailing in this boat, consider the following 

1. Greet the user with a welcome message at the beginning of the conversation and assume that user may reply with small talk like "thanks", "hello". 
2. Always end the conversation with small talk like "bye", "see you soon" etc. and assume that user will respond with similar words
3. Messaging is inherently slow and full of latency so it's possible that user become impatient when they do not see a response from the bot in time. Some user may try to talk to the bot using a word like "Hi", "Still there?" while the bot is still working on their previous request. It's best to handle such utterances appropriately. and make sure that you remove monotony from these responses. 

Small talk is a never-ending thing. There will never be enough of it. But if you look at it from your domain lens, you can come up with a reasonably small list of things that people can say that bot can reply in a friendly way. And for the rest, you can always have a number of variations of the same response (remember trait #3 - Do not be monotonous)

## #5 - Handle out of context conversations to a reasonable degree
One of the best things about natural language interfaces is that users get the freedom to express in whatever way they want. But this also becomes one of the biggest pain points for us, bot developers. Now, we have to deal with users who change the conversation context in the middle of a conversation. Let's look at an example of a hotel finder bot

```
Bot: Welcome to hotel finder. Where are you looking to travel?
User: I am looking for a room for 2 in Dubai next week
Bot: Sure thing. Let me find the best room for you
Bot: What do you think of the following options?
...
User: how long before I can cancel a booking?
```

The conversation was in the middle of a context around hotel search. User asks a question about the cancellation. The best thing for the bot to do here is to answer the user's question on cancellation (if modelled to do so) and then go back to hotel search. Microsoft bot framework supports such use cases out of the box. With others, you will need to do some work yourself but this is definitely possible. 

Handling out of context conversation is important because when the user makes a typo that results in bot not recognising what the user is saying, then you would want to present a friendly message to the user and then get back into the previous conversation context. 

## #6 - Use sentiment analysis tools to determine user's mood
The whole natural language understanding field is in its infancy still. The lack of maturity in the technology makes it difficult to build bots that can match a human's speaking abilities and wit. So there will be times when you will leave a customer unhappy, frustrated or angry. Use sentiment analysis tools on every user statement to understand user's mood and respond accordingly. Do not wait for an angry or frustrated customer to tell you that they want to speak to a human. Do not forget to ask a happy customer for their feedback. 

## #7 - Handoff to a human before the conversation becomes too frustrating for the user
Make it easy for human agents to take over a conversation from the bot. Make it easy for humans to switch from the bot to a human (e.g. when they type help). Make it easy for the bot to hand the conversation over to a human agent. 

You may not want to bake all of the above into your bot from day 1. But at least give the users an option to switch from a bot to a human, to begin with. Analyse how your users are interacting with the bot and decide what is the right time to get the other two features. 

## #8 - Offer a help menu
Last but not least, offer a help menu in the form of a conversation. The simplest thing you can do is when the user types something like "help" or "I need help", you can present a message back to the user listing everything that the bot can help the user with. In this response, you can also describe how to talk to a human. 

Again, Microsoft bot framework offers such feature out of the box. For other services, you will need to build this yourself. 

