---
title: Detailed Authorisation Code flow
keywords: homepage
sidebar: overview_sidebar
permalink: Impguide_DetailOverview.html
toc: true
summary: This page details the Authorisation Code Flow 
---

## Introduction

The diagram below shows the detailed Authorisation Code Flow.

### Detailed Authorisation Code Flow Sequence Diagram

![Detailed Auhentication code Flow Sequence Diagram](images/DetailedAuthorisationCodeFlow.jpg)


### Detailed Authorisation Code Flow Description

| Step| Description|
| ----- | --------- |
|1| The end user prepares the authentication request by entering the user credentials stipulated by the security policy of NHS.|
|2| The Relying Party will validate end user against the credentials held its local user database.|
|3| The Relying Party will redirect the User Agent to Authentication Server.|
|4|When a Relying Party requires that an End-User is authenticated they should cause a HTTP GET request over TLS to be sent from the End-User’s user agent to the OpenID Provider’s authorisation endpoint. The request may be generated indirectly via a HTTP 302 redirect response (for example in response to a user attempting to access a protected resource) or directly e.g. as a result of a login button being hit. The following parameters muist be included in the access request: **Response_Type = code**, **Scope=openID**, **Profile**, **Email**, **Client_id**, **Redirect_uri, state**|
|5|The Authorisation Server will ask consent from the User.  |
|6|It is optional for the User Agent to grant consent.  |
|7| The Authorisation Server of the Identity Provider will return an ‘`authorisation code`’ to the User Agent. |
|8| The User Agent will redirect the `authorisation code` recieved from the Authorisation Server onto the Relying Party.  The `authorisation code` acts like a **key** to make further requests. |
|9| The Relying Party can either request an [ID Token]  for authenticating a user  or an [Access Token] for authorisation access to a resource |
|10| The `authorisation code` provided by the Relying Party will be validated against the  the Identity Providers `token store database`. |
|11| Depnding on the request the [`Token Endpoint`](GlossaryTerms.html) will return an [ID Token] or an [Access Token].  If it is an `authentication request` then an [ID Token] will be returned and if it is an `authroisation request` an [Access Token] will be returned. |
|12| Ther Relying Party will validate the ID or the Access Token against the identity information held on its local identity data store. |
|13| The relying party will request for additional information about the user in the form of claims.  The [Access Token] will be included in request for the additional information. |
|14| The Authorisation Server will validate the [Access Token]. |
|15| The Authorisation Server will request additional claims from the user store. |
|16| The user end point will send the additional claims requested |
|17| Upon receiving the additional claims for the user the Relying Party will request `access` to the resource.  An [Access Token] is included in the request for Resources. |
|18| The Resource Server will validate the [Access Token] received from the Relying Party against the `access code` held for the Relying Party..|
|19| The Resource Server can request additional claims from the Authorisation Server. |
|20| The Authorisation Server will validate the [Access Token] against the `Token Database` held by the Authorisation Server. |
|21| The Authorisation Server will redirect the additional claim request to the User Endpoint. |
|22| The [`User Endpoint`](GlossaryTerms.html) will return additional claims to the - Resource Server |
|23|  The Resource Server will grant access by returning the resource to the Relying Party|
|24| The Relying Party will grant resource access to the End User.|

---

In the next few sections, we will walk through in detail looking at the key implementation of the Client/Relying Party/ User-Agent Operation used within the Authentication and Authorisation Service using Java and Python.






[ID Token]: <TechOverview_Artefacts.html#id-token>
[Access Token]: <TechOverview_Artefacts.html#access-token>