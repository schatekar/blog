---
layout: post
title: Treat the consumers of your API like a black box
excerpt: A lot of times we build an API to meet a specific need, publish those APIs and then expect the consumers to use the API for that specific purpose. This may work when both API producers and consumers are the same team. But the moment API consumption goes outside of the team, it becomes difficult to dictate how the consumers must use the API. It is best not to make any assumptions around that. 
tweet: Avoid arguments with consumers of your API over how to use the API
published: false
---

Recently we found out that an API that was built to help deliver a front-end feature was being used by another team for reporting. Initially, this was not a problem, but as the size of the database grew, we started seeing the impact it had on performance and throughput of this API. One suggestion in the room was to get to the team to stop using the API for that purpose. 

How do you deal with a situation like this? Definitely not by asking the other team to stop using this API to build reports. Who knows, tomorrow it will be some other team doing some other thing with this API. The answer is in building a level of protection in your API such that any use of this API will not result in unwanted performance or throughput degradation. The following simple feature additions will give you that protection. 

## #1 - Limit the number of results in a response

An API that returns unbounded result set affects the performance and throughput in more than one way. [This old post quite nicely and succinctly explains why unbounded result sets are plain wrong](https://ayende.com/blog/4785/what-am-i-so-hung-up-on-unbounded-result-set). Besides the out of memory exception and the bandwidth charges, imagines what it does to the performance and throughput of your API

1. The database takes longer time to process the query and return the results potentially affecting database performance and thus the performance of other applications connecting to that database
2. The API is taking longer time to process the unbounded result set thus affecting the overall performance of the API
3. It takes longer time to send the response resulting in the HTTP connection remaining open for longer time. This affects the overall throughput of the API.

As a rule of thumb, never let your the consumers of your API request an unbounded result set. Always ask for one or more parameters to filter the results and make those parameters mandatory or use default values for those parameters. If the API still returns a large number of results, then  limit this by implementing a pagination feature. If you have pagination feature, keep it on by default.  

## #2 - Limit the response payload
An over-sized payload has a similar effect on the performance and throughput as does the unbounded result set. A larger payload almost always takes up more processing power affecting the performance. It also has similar effect on the open HTTP connection result in reduced throughput. 

The most sophisticated way to limit the payload size is to [use hypermedia](https://martinfowler.com/articles/richardsonMaturityModel.html#level3). If you have never used hypermedia before, they it may sound overwhelming at first. There are specifications like [HAL](https://tools.ietf.org/html/draft-kelly-json-hal-08) and [Collection+JSON](http://amundsen.com/media-types/collection/) that make this a lot easier by formalising a lot of things. If you still feel too overwhelmed by hypermedia, then try giving [Lazy Gets](http://chatekar.com/take-your-hypermedia-api-to-the-next-level-by-using-lazy-gets/) a try. If you have ever used an ORM like Hibernate then you will find it easy to understand [Lazy Gets](http://chatekar.com/take-your-hypermedia-api-to-the-next-level-by-using-lazy-gets/). Lazy Gets by default return the minimal payload in response. If the consumer wants more than what's returned by default, they can explicitly request the additional data. If you want a rogue consumer from not requesting a lot of data too frequently then you can easily put access control around who can request what data easily.  They are a good stepping stone towards hypermedia APIs. 

## #3 - Throttle API calls 

## #4 - Prevent spikes in API calls
