---
title: Why you should use standard HTTP methods when designing REST APIs
published: true
excerpt: One of the characteristics of a good REST API is that it uses the standard HTTP methods in a way they are supposed to be used. We hear this all the time and this is the most fundamental guideline of REST.But beyond the basics, why is it like that? 
cover_image: http://i.imgur.com/863Sq0v.png
tags: rest, http, api
---

One of the characteristics of a good REST API is that it uses the standard HTTP methods in a way they are supposed to be used. We hear this all the time and this is the most fundamental guideline of REST. As generally understood, we use the following HTTP methods while designing REST APIs

 - **`GET`** — For returning resources
 - **`POST`** — For creating a new resource
 - **`PUT`** — For updating a resource
 - **`PATCH`** — For updating a resource
 - **`DELETE`** — For deleting a resource

But beyond the basics, why is it like that? Isn’t use of two methods, `PUT` and `PATCH` for an update operation confusing?

# What do the specs say?

Let’s first get the obvious out of the way. Let’s see what the specs say

### [GET](http://httpwg.org/specs/rfc7231.html#GET)
> The `GET` method requests transfer of a current selected representation for the target resource.` GET` is the primary mechanism of information retrieval

What this really means is that you should use `GET` for an API method that returns the latest version of the resource identified by the API URL.

### [POST](http://httpwg.org/specs/rfc7231.html#POST)
> The `POST` method requests that the target resource process the representation enclosed in the request according to the resource’s own specific semantics.
This is slightly confusing but that is because `POST` can be used to do more than one thing — one of which is creating a new resource. 

This is confusing because if the server can perform more than one operations in response to a request then how do consumers find out what happened exactly? The specification says that the server should make use of one of the 2xx family of status codes to indicate to the client what happened on the server.

### [PUT](http://httpwg.org/specs/rfc7231.html#PUT)
> The `PUT` method requests that the state of the target resource be created or replaced with the state defined by the representation enclosed in the request message payload.

So `PUT` can be used to update a resource as well as to create a new resource. That may sound strange at first, but let’s keep things simple for now and trust we should use `PUT` for an API method that lets consumers update the resource identified by the API URL.
### [DELETE](http://httpwg.org/specs/rfc7231.html#DELETE)
> The DELETE method requests that the origin server remove the association between the target resource and its current functionality.

Again, like `POST`, `DELETE` can be used for more than one operations that eventually result in something being removed. Let’s trust we should use `DELETE` for an API method that lets consumers delete the resource identified by the API URL.
### [PATCH](https://tools.ietf.org/html/rfc5789#page-3)
The difference between the `PUT` and `PATCH` requests is reflected in the way the server processes the enclosed entity to modify the resource identified by the Request-URI. In a `PUT` request, the enclosed entity is considered to be a modified version of the resource stored on the origin server, and the client is requesting that the stored version be replaced. With `PATCH`, however, the enclosed entity contains a set of instructions describing how a resource currently residing on the origin server should be modified to produce a new version.

`PATCH`, like `PUT`, should be used for modifying a resource, however, the semantics of modification is performed as slightly different. We will get to this difference in the next section.

So our original understanding of what each of the HTTP verbs means is in line with what the specifications say what they mean. So far so good. Specification tells us in which situations we should we use each verb, but it’s still just a specification. Our implementation can still disregard what the specification tells us to do and have the creation of new resources implemented behind a `GET` operation and deletions implemented a POST operation. However, there are two big benefits to respecting the specification.

# Idempotence is not limited to mathematics
In mathematics, an idempotent operation is one which produces the same result every time it’s performed on the same input. A counter is a good example of this. The operation to “set the counter to 6” is idempotent but the operation to “increment the counter by 1” is not. You see the difference? In the first case, no matter how many times you set the counter to 6, it’s still set to 6 in the end. Whereas, in the second case, if the counter had an initial value of 4 and every time you increment it by 1, the counter gets set to different value.

Applied to REST, an idempotent operation is the one which does not change the target state of the server. On the other hand, a non-idempotent operation would always change the target state of the server. Notice that we are not talking about state change here but rather the target state of the server. HTTP specification states that `GET`, `PUT` and `DELETE` are idempotent operations. `POST`, and `PATCH` are non-idempotent operations. “Like earlier, this is just a specification. Why do you need to follow it?” you might ask. Well, there is a reason and a very good one.

An idempotent operation gives the consumer of the API a guarantee that the state of the server will be the same no matter how many times they call the API. This guarantee is very useful. Imagine that server executes the API method that consumer called successfully but there is an error while sending the response back to the consumer. The consumer ends up getting an error even though the operation has completed successfully on the server. What should the consumer do? Now, if the operation server performed was advertised as idempotent, then A consumer can send the request to execute the operation one more time. It can keep doing that as long as it sees a success response without causing the server to perform any unwanted state change. On the other hand, if the operation was not advertised as idempotent then the consumer would know that it needs to check with the server before performing the operation again.

Creation of a new resource is one operation which changes the target state of the server every time it is run with the same inputs leading to a different target state after each execution. Same may apply to deletion of a resource depending on the implementation. Imagine what would happen if we put these operations behind a `GET` or a `PUT` verb? A consumer may end up executing these operations multiple times inadvertently affecting the target state of the server negatively. Returning value of a resource, on the other hand, has no impact on the target state of the server and hence should be implemented behind an idempotent verb `GET`.

There still is a difference between a `PUT` and a `PATCH`. Both are used to modify an existing resource. If you go back to what specification says about `PUT` you would notice that its similar to saying “set the counter to 6”. `PUT` is modifications where the consumer provides the target state for the complete resource and instructs the server to replace whatever value the resource has currently with the new value the consumer is sending. No matter how many times the consumer performs this operation, the end state of the resource is never going to change. `PATCH`, on the other hand, is similar to “increment the counter by 1”. `PUT` can be chunky for resources that are large in size and eats away a lot of bandwidth. `PATCH` was introduced to let consumers issue an instruction to the server that tells it how to change a part of the resource. This instruction, if executed multiple times, could result in an unwanted end state.

In the end, it’s all down to the implementation but if your implementation respects the specification then the life of your API clients would be a lot easier. While we are talking about respecting the specification, there is another interesting characteristic that the specification says all HTTP servers and proxies should build when dealing with HTTP request. Your REST API that respects the specification can make good use of this.

# Web is fast because of caching

The web is probably one of the heaviest users of cache. It not only makes loading of websites faster, it also works so reliably that not making use of it when it’s at our disposal would be foolish. REST uses HTTP and so it should make use of its caching characteristics where possible. The HTTP cache specification is quite detailed about how it should be implemented by HTTP servers and proxies but I would like to pick two things from the specification that directly apply to REST.

1. An operation behind a `GET` endpoint does not change the target state of the server, therefore, the response of a `GET` endpoint can be cached resulting in further requests to the same endpoint being returned faster from the cache
2. An endpoint behind `PUT`, `POST`, `PATCH` and `DELETE` changes the target state of the server, therefore, a successful response out of any of these endpoints can be used to bust the previously cached responses.

I know that I am overly simplifying the caching specification of HTTP but this is one of the most elegant caching specification I have come across. And all it takes to take full advantage of this to respect the HTTP specification.

One last thing about caching that impacts the consumers of an API more than the developers of the API. An API that follows HTTP Cache specification is the most useful to a consumer as long as the consumer uses an HTTP client library that supports caching. I am sure there is at least one such library available for every leading programming platform. So encourage your consumers to use one of those libraries. Having said that, API developers should still make use of caching as HTTP and proxy servers will still cache the responses.

# In closing

The Beauty of the HTTP API (and I am intentionally avoiding the word REST here) is that it provides a lot of flexibility to the API developer. Any flexibility is a good thing as long as it’s not misused. I have seen many HTTP APIs that either does not make use of recommended HTTP methods or if they do, the developer has little knowledge of why he made those choices. I hope this post throws some light on why we should use recommended HTTP methods.
