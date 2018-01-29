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

### Detailed Authorisation Code Flow

![Detailed Auhentication code Flow Sequence Diagram](images/DetailedAuthorisationCodeFlow.jpg)


### Detailed Authorisation Code Flow Description

| Step| Description|
| ----- | --------- |
|1| The end user prepares the authentication request by entering the user credentials stipulated by the security policy of NHS.|
|2| The relying party will validate end user against the credentials held its local user database |
|3| The relying party will redirect the User-Agent to authtication server|
|4|When a Relying Party requires that an End-User is authenticated they should cause a HTTP GET request over TLS to be sent from the End-User’s user agent to the OpenID Provider’s authorization endpoint. The request may be generated indirectly via a HTTP 302 redirect response (for example in response to a user attempting to access a protected resource) or directly e.g. as a result of a login button being hit. |
|5|  |
|6|  |
|7| ... |
|8| ... |
|9| ... |
|10| ... |
|11| ... |
|12| ... |
|13| ... |
|14| ... |
|15| ... |
|16| ... |
|17| ... |
|18| ... |
|19| ... |
|20| ... |
|21| ... |

In the next few section we will walk through in detail looking at the key implementation of the Client/Relying Party/ User-Agent Operation used within the Authentication and Authorisation Service using Java and Python.
