## Last Mile Security

As API developers we often tend to focus more on building what we think are the most secure APIs. We give little to no recognition of the fact that we have very little control over how the consumers of the API are going to treat the API keys, secrets and tokens that our APIs issue. 

In this talk, I will go over the story of an API developer. Let's call him Joe. Joe has developed a public API for the first time. Having built internal APIs in past, Joe's first choice to secure the new APIs is to use API keys. But Joe soon realises that he has little control over how the consumers of the API are handling this key. If the key gets stolen then it would probably be a long time before Joe can even know. Joe does some digging and figures out that APIs can be better secured using a token-based system like OAuth 2.0 or OpenId Connect. Joe still cannot control how the tokens get handled but Joe is able to control the damage by limiting the time that tokens are valid for. It just so happens, Joe now has an API consumer in the form of a mobile app. The developers of this App want tokens to live longer so that they can offer a seamless user experience. Joe is back to square one now. It would be long  before Joe can find out if these long lived token are stolen. 

Joe wants to be able to do more to protect his APIs than just asking the front-end developers to follow the best security practices. there are a few things Joe can do. For browser-based clients, Joe can accept only the requests where token is present in both a cookie and the header of the request. This will protect the API in case of there being an XSS/CSRF vulnerability in the client application. For the smartphone clients, John can setup a cryptographic challenge .. 

## Option 2

Software are designed radically differently these days. Mobile apps, single page applications, voice applications are becoming common. Consequently, we are developing more APIs than we ever developed before. More and more developers are producing APIs open for external consumption. Such use cases demand that API security be handled differently. We have moved from static key based authentication to token based authentication. We have moved from using custom token schemes to standards like OAuth 2.0 and OpenId Connect. However, the client applications consumings the APIs are being run in more and more untrusted environments. When a single page application gets hold of an API token, the API developer has no control over how this token is being protected while in the browser. APIs using bearer token authentication schemes are susceptible to misuse by someone who manages to steal a token because the client application did not store it securely. Even worse, because the token service was attacked to steal tokens. API developers need more weapons in their arsenal to protect APIs in such situations. 

In this talk, I will go over different mechanisms used to protect APIs, which aspect of the API security do they meet and where do they fall short. I will discuss different security threats posed by the new breed of client applications. Most importantly, I will talk about security mechanisms that will help API developers protect APIs without having to worry about how untrusted client applications are handling tokens. These range from old knowledge like correct use of cookies and CORS settings to latest guidelines like proof of possession tokens and challenge-response schemes. 

I call this last mile security. 

## Points

1. API key
2. API key and secret
3. Tokens
4. OAuth/OIDC
5. Long lived tokens
6. 