---
title: Implementing Authentication -  OpenID Connect
keywords: explore, design, reference
sidebar: overview_sidebar
permalink: ImpGuide_OIDC.html
summary: A detailed description of the NHS Digital implementation of Authentication OpenID Connect.
---

## Introduction

Authentication involves the identification of the users claim: proving who the user is before the Authorisation Service is initated.  
At the end of a successful authentication processThe outcome of the authentication service is to for the End User/ Relying Party to obtain an
> * **Authorisation Code**
> * **ID token (if the client doesn’t have one)**
  
This section is a guide to implemntation of Authentication and Authorisation using Java and Python as a language of choice of for NHS Digital DDC.

[//]In this section we will walk through the various requests and response messages relating to Authenticaltion and Authorisation with example code.


### Authentication Request

|**Description**| The authentication request is done by redirecting the end user to the provider, for more details see the OIDC specification. The redirect URL is built as follows, using the Authorization Code Flow.| 
|**Protocol example**| |
|**Coding Example**|  [Java Example](ImpGuide_AuthReq_Java.html), Python click Here |
|**Supporting Information**| If the provider does not support the discovery protocol, replace providerMetadata.getAuthorizationEndpointURI() with the authorization endpoint URL received out-of-band.	If the provider does not support dynamic client registration, replace clientInformation.getID() with the client id received out-of-band. Make sure redirectURI matches a URI known by the provider. The state and nonce should be stored so they can be retrieved later. |

### Authorisation Code

|**Description**|The authentication response is sent from the provider by redirecting the end user to the redirect URI specified in the initial authentication request from the client. The Authorization Code can be extracted from the query part of the redirect URL|
|**Protocol Example**| ..|
|**Coding Example**| [Java Example](ImpGuide_AuthCode_Java.html) Click here,  Python click here |
|**Supporting Information**| When using either implicit or hybrid flow the authentication response is encoded in the fragment part of the URL. This requires additional handling, e.g. using Javascript, see Implementation Notes. After receiving the response back in the client, it can be parsed in the same way as when using Code flow (Note: we don’t need to include this)|


## ID Token

### ID Token Request

|**Description**|The ID token resembles the concept of an identity card, in a standard JWT format, signed by the OpenID Provider (OP). To obtain one the client needs to send the user to their OP with an authentication request.|
|**Protocol Example**| ... |
|**Coding Example**| [Java Example](ImpGuide_IDTOkenReq_Java.html), Python click here |
|**Supporting Information**| When an authorization code (using code or hybrid flow) has been obtained, a token request can be made to get the access token and the id token  |

### Validate ID Token

|**Description**|The id token obtained from the token request must be validated, see  OpenID connect for ID token validation.|
|**Protocol Example**| ..|
|**Coding Example**| [Java Example](ImpGuide_Val_IDToken_Java.html),  Python click here |
|**Supporting Information**| ..|
