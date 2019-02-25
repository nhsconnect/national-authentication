---
title: Authorisation Service Overview
keywords: homepage
sidebar: overview_sidebar
permalink: Intro_Authorisation.html
toc: true
summary: A brief introduction of the Authorisation Service within NHS Identity Service.
---

![Authorisation image](images/IntroAuthorisationService.JPG)


Authorisation is the process which determines whether a digital identity has sufficient privileges to access resources protected by that service.

NHS Identity’s Authorisation service can protect web pages, web services and API’s. The Authorisation solution refers to policy engine to decide what rules are set for access to a protected resource. Each resource will have several scopes that define the type of access that can be given to a client subject on that resource e.g. Patient Record Read, Patient Record Write etc.

NHS Identity authorisation service primary purpose is to protect national services such as Patient Demographic Services, Summary Care Record, Electronic Referral Service etc.

NHS Identity authorisation service offers the below benefits:

> * Abstracts access rules into a centralised policy engine which can be amended by configuration
> * Provides standards based access control with built-in consent (OAuth 2.0)
> * Provides short lived Access tokens & Refresh Tokens to enable efficient and secure access to resources
> * Provides policy agents which intercept and redirect traffic for authentication and authorisation

