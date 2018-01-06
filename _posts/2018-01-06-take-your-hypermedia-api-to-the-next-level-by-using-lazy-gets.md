---
layout: post
title: Take your hypermedia API to the next level by using Lazy Gets
excerpt: One of the challenges of building any public API is that you do not know who will use your API, or how they will use it. That also means you cannot make assumptions about some aspects of the API. One such aspect is size of the payload. A number of factors specific to the business domain and API implementation will decide the size of the payload. However, it will be wrong to say that the consumers have no role to play in this. API consumers would want to be able to fetch just the enough data from any API. This saves them network bandwidth and processing of unnecessary payload. 
tweet: Take your hypermedia API to the next level by using Lazy Gets
published: true
---

One of the challenges of building any public API is that you do not know who will use your API, or how they will use it. That also means you cannot make assumptions about some aspects of the API. One such aspect is size of the payload. A number of factors specific to the business domain and API implementation will decide the size of the payload. However, it will be wrong to say that the consumers have no role to play in this. API consumers would want to be able to fetch just the enough data from any API. This saves them network bandwidth and processing of unnecessary payload. 

## Welcome the "Lazy Get"

Most Object Relational Mapper(ORM) tools have a feature called Lazy Loading. ORMs use this feature to return only the top level entity when they execute a SQL script. Any associated entities are not loaded completely but only their identifiers are loaded. When the application tries to access the associated entity, the ORM kicks in. It loads that entity using its identifier which it had loaded earlier. This is smart because ORM is not guessing when the application needs what. Instead, it is giving the application an ability to fetch on demand what’s needed when.

Lazy Get is similar. With Lazy Get, you do do not return a linked resource by default. Instead, you return a shallow version with only top level attributes populated. The API consumer can

1. Instruct the server to return the linked resources in the same response
2. Retrieve the linked resources at a later time using the link returned in the original response

This is best explained with an example. Let’s say we are building a meetup platform. People can create interest group and host meetups using our platform. Members of the platform can

1. Join the groups they like
2. Connect with other members of the platform
3. RSVP for the events hosted by various groups

This is a set of basic features any meetup platform can have.

This platform is API enabled and we have got an API method to retrieve a `member` resource which looks like below.

```json
{
  "id": 34234,
  "firstname": "Suhas",
  "lastname": "Chatekar",
  "email": "abc@gmail.com",
  "memberships": [{
    "meetup_id": 2345,
    "name": "London Erlang Group"
  }],
  "rsvps": [{
    "event_id": "546",
    "number_of_attendees": 2
  }],
  "friends": [{
    "id": "5678",
    "since": "12/05/2015"
  }]
}
```

For brevity, the above code does not show the full representation of `memberships`, `rsvps` and `friends` resources. In reality, these resources will have more attributes than what I am showing here. They could even have their own linked resources.

A consumer of this API may not need all of this data all the time. A consumer connecting over LAN would happily accept a lot of data returned. But a mobile app developer connecting over a slow internet connection would not want this. Guess what? You can implement Lazy Get on this API method and let the consumer decide what data they want to be returned. You do this by supporting a new query parameter named `expand`. This parameter accepts comma separated names of the linked resources that the consumer wants the server to return. So for example, if the URL for retrieving the above member resource was

```
https://myapi.com/v1/member/34234
```

If a consumer wants only memberships information returned then they can send a request to the following URL

```
https://myapi.com/v1/member/34234?expand=memberships
```

This is good. Now the consumer has a control over what data server returns. But what happens to other resources i.e. rsvps and friends? Is server just going to exclude them from the response? If server excludes them how does the consumer get those resources when it needs them?

Instead, what server does is exactly same as what any ORM does with its lazy loading feature. The server returns an identifier of the resource in the place of the full resource

```js
{
  "id": 34234,
  "firstname": "Suhas",
  "lastname": "Chatekar",
  "email": "abc@gmail.com",
  "memberships": [{
    "meetup_id": 2345,
    "name": "London Erlang Group"
  }],
  "rsvps": [{
    "event_id": "546" //Only identifier of the resource. No other details
  }],
  "friends": [{
    "id": "5678" //Only identifier of the resource. No other details
  }]
}
```

That way, if the consumer decides to fetch `rsvps` or `friends` resources, all they need to do is issue a `GET` request on the corresponding URLs.

## Using hypermedia to make this little better

In the previous example, how would a client fetch a `friend` resource with id 5678? Where would it get the actual URL to fetch this resource from?We can use [hypermedia](https://en.wikipedia.org/wiki/HATEOAS) to help us here. If you have used hypermedia before then you may have guessed what I am talking about.

You can use one of the hypermedia specifications like [Siren](https://github.com/kevinswiber/siren), [HAL](https://tools.ietf.org/html/draft-kelly-json-hal-08) or [Collection+JSON](http://amundsen.com/media-types/collection/) to return actual URL for the resource instead of just the id. If you are still at [Richardson Maturity Model — Level 2 or below](https://martinfowler.com/articles/richardsonMaturityModel.html), don’t worry. You can do what we have done in such cases. We do not return the identifier of the linked resource. For out clients, it does not mean anything. We instead return an attributed `href`. This attribute contains the URL on which the clients can send a `GET` request to fetch that resource. The below is how our `member` resource looks with `href` attribute returned.

```js
{
  "href": "https://myapi.com/v1/member/34234",
  "id": 34234,
  "firstname": "Suhas",
  "lastname": "Chatekar",
  "email": "abc@gmail.com",
  "memberships": [{
  "href": "https://myapi.com/v1/meetup/2345",
    "meetup_id": 2345,
    "name": "London Erlang Group"
  }],
  "rsvps": [{
    "href": "https://myapi.com/v1/event/546"
  }],
  "friends": [{
    "href": "https://myapi.com/v1/member/5678"
  }]
}
```

And we return this attribute by default for all our resources.

## Happy API consumer == Happy API developer == Great API
A product becomes great when their users are happy using that product. The same is true about APIs. 

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Treat your API like a product. Provide a good developer experience and have continuous, proactive engagement with consumers. <a href="https://twitter.com/hashtag/GartnerCAT?src=hash&amp;ref_src=twsrc%5Etfw">#GartnerCAT</a></p>&mdash; Gartner Events (@Gartner_Events) <a href="https://twitter.com/Gartner_Events/status/766024242953465856?ref_src=twsrc%5Etfw">August 17, 2016</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>


I think that tweet sums it all. Lazy Gets is one of the ways to enhance the experience for the users of your APIs. Use it when you can. And use every other feature that will make your API product awesome. 