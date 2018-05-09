---
title: Key Terms and Conepts used within NHS Identity
keywords: homepage
sidebar: overview_sidebar
permalink: Tech_KeyTerms.html
toc: true
summary: A brief definition of Key Terms/Concepts for NHS Identity.
---




### Key Terms/Concepts

The following key terms are used in the rest of site:

* **Claim**

  A piece of information asserted about an entity. OpenID Connect defines a number of standard claims e.g. the name claim represents an End-User's full name in displayable format.
  
* **Scope**

  A collection of claims. OpenID Connect defines a number of standard scopes that a Relying Party can request about an authentication event or End-User. For example the profile scope contains claims such as: name, family_name, given_name etc.

* **ID Token**

  A JSON Web Token ([JWT](https://tools.ietf.org/html/rfc7519)) that contains claims about the authentication event and may contain claims about the End-User. An ID Token is requested using the openid scope.

* **Access Token**

  A credential used to access protected resources. Access tokens represent specific scopes and durations of access.
   
* **Refresh Token**

  A credential used to obtain access tokens.  Refresh tokens are issued to the client by an authorization server and are used to obtain a new access token when the current access token becomes invalid or expires.
   
* **UserInfo Endpoint**

  A protected Resource that, when presented with an access token returns information about an End-User.