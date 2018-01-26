---
title: Registering a User
keywords: homepage
sidebar: overview_sidebar
permalink: ImpGuide_Reg.html
toc: true
summary: This section provide a guide on registering a user  
---

(this section is still under discussion – nick sykes)

Before being able to interact with an OpenID Provider a Relying Party must first register with the provider. During this process the following items will be exchanged:

> 1.	The URIs of the OpenID Provider’s authorization, token and user endpoints.
> 2.	An issuer identifier identifying the OpenID Provider.
> 3.	A mechanism for obtaining the OpenID Provider’s public keys.
> 4.	A client identifier uniquely identifying the Relying Party.
> 5.	The Relying Party’s redirection URIs to which responses may be redirected.
> 6.	A client authentication mechanism and associated credentials.

This may be achieved via manual means. However OpenID Connect also provides an electonic way of doing this.
