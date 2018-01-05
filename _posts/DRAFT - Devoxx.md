# Ensuring your APIs are secure

## Summary

As API developers, we often overlook the fact that the security requirements are also driven by how consumers are using our APIs. With more and more consumers building single page apps and mobile apps that directly access APIs from uncontrolled environments, the security of the API comes down to how secure these client applications are. It is not prudent to secure our APIs without understanding what kind of security risks exists in the new kind of front-end apps and how to protect against them. 

There seems to be a lot of confusion in the front-end community when it comes to securely handling API keys, secrets, token etc. Getting the right level of security in untrusted environments like user's browser or smartphone is not straight-forward. This talk will try to answer questions like what is the best mechanism to prevent tokens and secrets from being stolen? How to protect your APIs when secrets/tokens get stolen? How to prevent unauthorised actors from accessing your API?

-------
What should you use to secure your APIs? Are API keys enough? Do you need secrets too? Or JWTs the best option? 

As API developers, we always try to answer these questions. One the commonly overlooked aspect while answering these questions is that the security requirements of an API are mainly driven by how the consumers are using these APIs. If a consumer of your APIs is single page app that stores API key in local/session storage and has XSS vulnerability, then it would not matter if you use OAuth 2.0 or any other fancy protocol. This problem magnifies manifold if you are building public APIs with no visibility of what client apps are being built against your API. 

Do you have to rely on the developer of the client app making the right security decisions? Isn't there nothing we can do to protect our APIs despite the API consumers making a wrong security choice? How do you limit the damage when a breach happens? Come to this talk to get answers to these and similar questions. You will leave the session with a few design guidelines and tips that would take your API security to the next level. 


## Message to committee
I am the technical product manager for an IAM product that we are building here at Collinson Group. In this role, I get to speak to a number developers, architects and product managers. I speak to peers who are concerned about the security of their APIs. I speak to API developers who believe their APIs are secure because they have used the best token-based protocol like OAuth 2.0. What I often see missing in these conversations is any mention of last-mile security, the fact that, there front-end applications consuming these APIs are moving from classical server-side apps to single page apps and mobile apps. These new kinds of apps have limited options when it comes to protecting API secrets and tokens. The front-end developers working on these apps are mostly unaware of the security risks of storing sensitive security information in the local storage of a browser. On one hand, there is a need to educate front-end developers on these matters, on the other hand, API developers need to beef up their game by taking the responsibility for protecting their APIs despite the wrong security choices made by the consuming applications. 

There is a lot of good advice available on the internet but it is fragmented and difficult to find unless you know what you are looking for. And most developers do not know what they do not know. So actively seeking information on best API security practices is not a common phenomenon. There is a need for more coherent and complete material on this topic. There is a need for developer awareness and education on this topic. I am motivated to teach every developer I come across. I believe, with this talk, I would be able to reach out to a wider group of developers and help to build more secure APIs.  

This will be first public talk if I get selected. I do not want to withhold this information if it plays a role in selection. I have done internal talks at my organisation on various topics before, if that helps. 

