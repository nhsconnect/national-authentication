---
title: Registering a Client
keywords: homepage
sidebar: overview_sidebar
permalink: ImpGuide_Reg.html
toc: true
summary: This section provide a guide on registering a user  
---




(this section is still under discussion and `subject to change`)

![Under Construction](images/UnderConstruction.jpg)

Before using the NHS Digital implementation of OpenID Connect a third party will need to register their details. This is a manual step as Dynamic Registration is not supported
Before being able to interact with an OpenID Provider a Relying Party must first register with the provider. During this process the following items will be exchanged:

> 1.	The URIs of the OpenID Provider’s authorization, token and user endpoints.
> 2.	An issuer identifier identifying the OpenID Provider.
> 3.	A mechanism for obtaining the OpenID Provider’s public keys.
> 4.	A client identifier uniquely identifying the Relying Party.
> 5.	The Relying Party’s redirection URIs to which responses may be redirected.
> 6.	A client authentication mechanism and associated credentials.



During these steps the following values will be agreed:


|Value|	Description|
| -----| ----------|
|client_id|	An identifier for the third party application which will be allocated by NHS Digital e.g. abc123.|
|client_name|	A name for the third party application.|
|redirect_uris|The URI(s) to which the third party application may request authorization codes to be redirected. As noted above these will be custom URIs e.g. clientapp://connect/authresponse|
|jwks_uri|	The URI which the third party will us as a JWKS endpoint (see Key Management) e.g. https://client.example.org/.well-known/jwks.json.|


This may be achieved via manual means. However OpenID Connect also provides an electonic way of doing this, see the Discovery and Dynamic Registration sections in the the Other OpenID Connect Features page for further details.
Upon successful registration the Identity provider will issue the client with the following information:

> *	**Client Id** 
> *	**Secret Key**

These information will uniquely identify the Client.

Please note: At the time of writing Discovery and Dynamic registration is beyond the scope of CAS.
