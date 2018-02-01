---
title: 
keywords: homepage
sidebar: overview_sidebar
permalink: GlossaryTerms.html
toc: true
summary: 
---
![Glossary](images/glossary.jpg)

|or|

![Glossay Magnifying Glas](images/GlossaryMag.jpg)




This section defines the Glossary of Terms used within Care Access Service.


| Term | Definition |
| ------ | -------------|
| Subject| An active party that request access from an Object. | 
| Client | An application making protected resource requests on behalf of the resource owner and with its authorization.  The term "client" does  not imply any particular implementation characteristics (e.g., whether the application executes on a server, a desktop, or other devices).This is sometimes known as the Relying Party |
| Relying Party | The client application requesting End-User authentication and information about the End-User. This can also be referred to as a Client. |
| Authentication Server | The server issuing access tokens to the client after successfully authenticating the resource owner and obtaining authorization.  An OAuth 2.0 Authorization Server that is capable of authenticating an End-User and providing information to a Relying Party about the authentication event and the End-User. This is also refered as an OpenID Provider(OP) |
| Resource Owner | An entity capable of granting access to a protected resource.When the resource owner is a person, it is referred to as an end-user. |
| Resource Server | The server hosting the protected resources, capable of accepting and responding to protected resource requests using access tokens. |
| UserInfo Endpoint |A protected Resource that, when presented with an access token returns information about an End-User.  |
| Token Endpoint |A protected Resource that issues and stores Token and their respective information  |
|Claim|A piece of information asserted about an entity. OpenID Connect defines a number of standard claims e.g. the name claim represents an End-User’s full name in displayable format.|
|Scope|A collection of claims. OpenID Connect defines a number of standard scopes that a Relying Party can request about an authentication event or End-User. For example the profile scope contains claims such as: name, family_name, given_name etc. |
|ID Token| A JSON Web Token [JWT](https://tools.ietf.org/html/rfc7519) that contains claims about the authentication event and may contain claims about the End-User. An ID Token is requested using the openid scope. |
|Access Token| A credential used to access protected resources. Access tokens represent specific scopes and durations of access.|
|Refresh Token|A credential used to obtain access tokens. Refresh tokens are issued to the client by an authorization server and are used to obtain a new access token when the current access token becomes invalid or expires.|
