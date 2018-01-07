
## One line description

## Abstract:

This session is about API security in general with emphasis on techniques to protect APIs when secrets or tokens are issued to public clients. Public clients are applications that run in an untrusted environment. Examples include single page applications, mobile applications etc. 

In this session, I will go over different mechanisms used to protect APIs. I will discuss how these mechanisms work, which aspect of the API security do they meet and where do they fall short. I will also talk about different security threats posed by the public clients. Most importantly, I will talk about options that will help API developers protect APIs without having to worry about how public clients are handling tokens. These options range from old knowledge like correct use of cookies and CORS settings to latest guidelines like proof of possession tokens and challenge-response schemes.

There is a good understanding of general API security techniques among the developer community. However, most developers would not concern themselves with how untrusted client applications are handling the secrets or tokens issued to them. Single page applications are becoming the default choice when building a web application these days. These applications access APIs directly from the browser and rely on browser supplied storage options to store the sensitive information.  Vulnerabilities like XSS/CSRF in these applications mean that secrets or tokens may be stolen. Redirection attacks on identity servers also playing a part in this. Abundant use of unverified npm packages may result in XSS attack. If APIs are relying on bearer authentication then we are giving the bad guys a free ride. Anyone in possession of the token is able to successfully access the API. I believe that API developers must understand the environments in which their client applications are being developed and run. They need to be able to introduce additional security layers that protect their APIs against threats not under their control. 

## Audience background:

Knowledge/experience of building any kind of API would be helpful. Understanding of API security will be an added advantage

## Benefits of participating

 - Understand full API security landscape
 - Understand the roles performed by different actors and threats posed thereof
 - Make informed API security decisions

## Materials you'll provide

 - Slide deck
 - Links to important IETF standards
 - Links to useful articles and blog posts

## Process

This is a good old "slides and talk" kind of session with participation from the audience intermixed in the form of discussions. 

## Detailed timetable

75 minute session

5 minutes - Introduction
15 minutes - API security journey so far
15 minutes - Three actors in standard token based authentication
15 minutes - Security threats posed by the client applications
15 minutes - Security techniques available to API developers 
10 minutes - Any questions from audience

## Outputs:

 - Slides 

## History 

This session has not been presented anywhere yet. I have been talking about the ideas internally at my organisation and elsewhere but no formal presentation.