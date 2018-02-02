---
title: Authentication Service Overview
keywords: homepage
sidebar: overview_sidebar
permalink: Intro_Authentication.html
toc: true
summary: A brief introduction to the Authentication Service within Care Access Service.
---

![Authentication image](images/Authentication.jpg)


** Authentication is the process that ensures and confirms a subjects identity to a particular assurance level.**

The higher the assurance level the more confident a client system can be that the subject is who they say they are. 

A higher level of assurance can be gained in 1 of 2 ways:  a subject can use a highly trusted mechanism to prove their identity e.g. A biometric or a cryptographic secret or by adding many factors of proof together e.g. a password **and** a knowledge based secret **and** possession/sole ownership of a protected device such as a phone or smartcard.

The capabilities of the CAS Authentication Service are as follows:
* It can authenticate against around 1 million care worker identities in its repository; registered and checked to a high level of confidence (LoA 3 – Face to Face combined with passport, driving license checks)
* It has many new methods of verifying the subject: One Time Passwords, Push Notifications, Knowledge Based Secrets, Cryptographic Certificates and Smartcards
* Multi-factor authentication is supported 
* It can check contextual central rules pre and post authentication to reduce risk e.g. has this mobile device been linked to the user?,  is the location of the subject allowed (in UK)?, has the identity information for this user ever been captured by cyber attack?
* A single sign on cookie can be created and maintained to reduce user friction.
* A step up to a higher assurance of authentication can be triggered if a subject requests access to resources that require it
* It Audits authentications for adherence to governance
* It uses the OpenID Connect standard authentication protocol championed by technology giants Microsoft and Google.

