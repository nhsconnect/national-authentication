---
title: Detailed Authorisation Code flow
keywords: homepage
sidebar: overview_sidebar
permalink: Impguide_DetailOverview.html
toc: true
summary: This page details the Authorisation Code Flow 
---

## Introduction

The digram below shows the detailed Authorisation Code Flow.

### Detailed Authorisation Code Flow Sequence Diagram

![Detailed Auhentication code Flow Sequence Diagram](images/DetailedAuthorisationCodeFlow.jpg)


### Detailed Authorisation Code Flow Description

| Step| Description|
| ----- | --------- |
|1| The end user prepares the authentication request by entering the user credentials stipulated by the security policy of NHS.|
|2| The relying party will validate end user against the credentials held its local user database |
|3| The relying party will redirect the User-Agent to authtication server|
|4|When a Relying Party requires that an End-User is authenticated they should cause a HTTP GET request over TLS to be sent from the End-User’s user agent to the OpenID Provider’s authorization endpoint. The request may be generated indirectly via a HTTP 302 redirect response (for example in response to a user attempting to access a protected resource) or directly e.g. as a result of a login button being hit. The following parameters muist be included in the access request: **Response_Type = code**, **Scope=openID**, **Profile**, **Email**, **Client_id**, **Redirect_uri, state**|
|5|The Authorisation Server will ask consent from the user.  |
|6|It is optional for the User Agent to grant consent.  |
|7| The authorisation server of the identity provier will return an ‘authorisation code’ to the user agent. |
|8| The user agent will redirect the authorisationcode recieved from the Authorisation Server onto the Relying Party.  The authorisation code acts like a key to make further requests. |
|9| The Relying Party can either request an ID Token for authenticating a user  or an Access Token for Authorisation to a resource |
|10| The authorisation code provided by the relying party will be validated against the  the Identity Providers Token store database. |
|11| Depnding on the request the Token endpoint will return an ID token or an Access Token.  If it is an authentication request then an ID Token will be returned and if it is an Authroisation Request and Access Token will be return. |
|12| Ther relying Party will validate the ID or the Access ~token against the identity information held on its local identity data store. |
|13| The relying party will request for additional information about the user in the form of claims.  The Access token will be included in request for the additional information. |
|14| The authorisation server will validate the Access Token |
|15| The Authroisation Server will request additional claims from the user store. |
|16| The user end point will send the additional claims requested |
|17| Upon receiving the additional claims for the user the Relying Party will request Access to the resource.  An Access token is included in the request for Resources. |
|18| The Resource server will validate the Access token received from the Relying Party against the access code held for the relying party..|
|19| The ResourceServer can request additional claims from the Authorisation Server. |
|20| The Authroisation Server will validate the Access Token against the Token Database held by the Authorisation Server. |
|21| The authorisation server will redirect the additional claim request to the User Endpoint. |
|22| The user Endpoindt will return additional claims to the - Resource Server |
|23|  The resource server will grant access by returning the resource to the relying party|
|24| The Relying Party will grant resource access to the End User.|

In the next few section we will walk through in detail looking at the key implementation of the Client/Relying Party/ User-Agent Operation used within the Authentication and Authorisation Service using Java and Python.
