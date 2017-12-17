---
title: Return well-formed error responses from your REST APIs
published: true
description: Standard HTTP status codes are a good starting point to indicate error condition but they are not enough. Especially if you are developing APIs that are consumed by a large number of developers or are open to access by anyone then you may want to return well-formed error responses that provide more details about the error. 
tags: rest, api, apis
---

REST recommends using standard HTTP status codes to indicate what has happened on the server in response to a request. Errors from 4xx and 5xx family are used to indicate that request is not processed and there is some error either on the client side or on the server side e.g. 401 Unauthorised is used to indicate that the request cannot be processed because it does not anything to prove the identity of the sender. Standard HTTP status codes are a good starting point to indicate error condition but they are not enough. Especially if you are developing APIs that are consumed by a large number of developers or are open to access by anyone then you may want to return well-formed error responses that provide more details about the error. The initial inspiration for this idea comes from [Generate Structured Errors](https://geemus.gitbooks.io/http-api-design/content/en/responses/generate-structured-errors.html) chapter of the [GitBook HTTP API Design Guide](https://geemus.gitbooks.io/http-api-design/content/en/index.html). I personally recommend this book to anyone who wants practical advice on building REST APIs.
At [Collinson Group](http://collinsongroup.com) we have started returning JSON similar to the one below in some `4xx/5xx` responses

```
[{ 
  "errorCode": "BAD_FORMAT", 
  "field": "email", 
  "originalValue": "suhas.chatekar", 
  "mesage": "{email} is not in correct format",
  "helpUrl": "/help/BAD_FORMAT#email" 
  }]
```


The above JSON is returned in response body whenever we believe that the standard HTTP status is not enough for the calling application to know what has gone wrong. Let’s quickly see what purpose each of these fields fulfil and what values they may contain.

## errorCode
As the name suggests this field holds a unique error code. We decided to use string-based error codes as they are easy to read. People also use numbers for this. I personally feel that numbers are cryptic for this kind of information.

## field
Name of the field which has this error. This is the same name that appeared in the incoming request.

## originalValue
This field contains the original value from the request. This is optional in most cases. While the client can make use of this information if they need to, there is one situation where we found returning this information to be useful. We had a POST API that accepted an array of the same resources. If more than one resource fails the same validation on the same field then we end up returning same error response twice. How will the client know which resource was in error? Adding original value in the response helps track the client which resource in the request had an error.

## message
This field contains a user-friendly message. If the consumer of the API is a front-end application then it may choose to use this message directly to convey details of the error to the end user. There are two things to note around this field. One, the example above shows the message as tokenised with `{email}` as a token in the message. The API should replace this token with the original value from the request before returning the response. Two, this message should be localised in a language that client prefers. This assumes that you have got a mechanism in your API for your clients to specify a preferred language.

## helpUrl
This field contains URL to a page that describes this particular error in more detail. The help page may answer the following questions (in addition to any other details you may want to include)
1. What causes this error? Examples will help here.
2. How to fix this error?
3. If you continue to get the error, how do you get help?

I call this mechanism **discover-able documentation** because developers of the client applications do not have to know where to find this documentation when they encounter an error, they automatically discover appropriate documentation instantly.

## Error codes that we use
The following list of error codes satisfies most common field level errors.

|Error Code|Error Situation|Example|
|----------|---------------|-------|
|MISSING_FIELD_VALUE|Request does not contain the value of a field that is mandatory| |
|UNKNOWN_FIELD_VALUE|The value specified for a field is not recognised|Lookups, identifiers of linked resources etc.|
|BAD_FORMAT|The value specified for a field does not comply with a particular format| Email address, URLs etc.|
|INVALID_FIELD_LENGTH|Length of the value of a field is less than the minimum or more than the allowed length||
|DUPLICATE_FIELD_VALUE|Violation of unique constraint||


There are some domain-specific error codes we use that I have omitted. You can define as granular error codes as possible. Are you using well-formed error responses in your APIs? Do you find this approach useful?


