---
title: Federation Service Overview
keywords: homepage
sidebar: overview_sidebar
permalink: Intro_Federation.html
toc: true
summary: A brief introduction Federation within NHS Digital's Care Access Service.
---

Federation is the agreement between multiple organisations to trust an Identity Providers (IdP) digital identity token and allow access to resources within these organisation based on the attributes contained within it. 

In the context of the NHS Digital Service we will provide a digitally signed national care worker token which can be accepted by many NHS Organisations and 3rd party cloud services as proof of identity 

The capabilities of the CAS Federation Service are:

* OpenId Connect, SAML or WS-Federation Federated Identity (WS-Federation will allow seamless SSO access to Microsoft services such as NHSMail, Office 365, Skype)
* Secure Attribute Exchange for system to system identity data exchange
* Secure Token Service providing a means to exchange tokens across security domains without re-authenticating or re-establishing trust relationaships