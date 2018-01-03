## Last Mile Security

As API developers we often tend to focus more on building what we think are the most secure APIs. We give little to no recognition to the fact that we have very little control over how the consumers of the API are going to treat the API keys, secrets and tokens that our APIs issue. 

In the old days, when everyone was building classical server side websites, issuing a static API key was usually enough to ensure security of the API. It also worked for smart phone apps as breach of smart phone apps was not common. With rise of single page applications and increased vulnerability of smart phone apps, static API keys are becoming a dangerous proposition. Most developers are moving to token based API authorisation schemes like OAuth 2.0 and OpenId Connect but even they have their own best practices to be aware of. All said and done, any API security scheme comes down to protecting the tokens from being stolen or preventing stolen tokens from being used.   

In this talk, I will go over some of the common API security practices 