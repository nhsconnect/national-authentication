---
title: Authentication Service Overview
keywords: homepage
sidebar: overview_sidebar
permalink: Intro_Authentication.html
toc: true
summary: A brief introduction to the Authentication Service within NHS Identity Service.
---


![Authentication image](images/IntroAuthenticationService.JPG)


Authentication is the process that ensures and confirms a subject’s identity to a particular assurance level. The higher the assurance level, the more confident a client system can be that the subject is who they say they are. 

NHS Identity Authentication Service offers the following benefits:

> * NHS Identity currently authenticates against around 1 million care worker identities in its repository; registered and checked to a high level of confidence.
> * Has many new methods of verifying the subject: One Time Passwords, Push Notifications, Knowledge Based Secrets, Biometric touch id, Windows Hello, Cryptographic Certificates, FIDO2 supported devices, OIDC Smartcards etc.
> * Multi-factor authentication is supported.
> * NHS Identity can check contextual central rules pre and post authentication to reduce risk. e.g. has this mobile device been linked to the user? Is the location of the subject allowed (in UK)?, has the identity information for this user ever been captured by cyber-attack?
> * A single sign on cookie can be created and maintained to reduce user friction.
> * A step up to a higher assurance of authentication can be triggered if a subject requests access to resources that require it.
> * Audits authentications for adherence to governance.
> * Uses OpenID Connect standard authentication protocol championed by technology giants Microsoft and Google.
