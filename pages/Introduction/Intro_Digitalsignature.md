---
title: Remote Digital Signature Service
keywords: homepage
sidebar: overview_sidebar
permalink: Intro_Digitalsignature.html
toc: true
summary: A brief introduction to the Digital Signature Service within NHS Identity
---
For a long time, transactional e-services have been designed for typical end-user devices such as desktop computers and laptops. Accordingly, existing digital signature solutions are tailored to the characteristics of these devices as well. This applies to smart card and USB token-based solutions. These traditional signature solutions implicitly assume that the user accesses e-services from a desktop or laptop computer and in addition uses a smart card or token to create any required digital signatures. This assumption is not valid any longer. During the past few years, smartphones, tablets and other mobile end-user devices have started to replace desktop and laptops computers.

This situation raises several challenges for e-services: smart cards and tokens cannot be easily connected to smart phones and other mobile devices, or cannot at all. For instance, smartphones usually do not provide support for USB devices, which is the common technology for smart card based solutions.

In this regards, recent regulations in various regions worldwide – like eIDAS in the European Union – have introduced the concept of electronic signatures that are created using a “remote signature creation device”, which means that the signature device is not anymore a personal device under the physical control of the user, but rather it is replaced by cloud-based services offered and managed by a trusted service provider.

User signing keys and certificates are stored centrally, protected via a certified HSM (Common Criteria EAL4+ certified according to EN 419221-5 Protection Profile). There is no need to deploy expensive Smartcards and Readers, or even USB tokens. Users can easily sign using any device without installing specialist software.

**Benefits of this Approach:**

Strong Authorisation : The signer is requested to authorise all signing transactions involving their signing key via notification to their registered device. The signer authorises the transaction by using a FIDO2 backed biometric authentication built into the iOS, Android or Windows tablet device. A digitally signed authorisation message which cryptographically binds the signed document, user’s ID and the registered mobile device biometric.

Device Assurance : The user can only authorise transactions from their pre-registered assured devices.

Secure Logging : The signed authorisation response from the user’s mobile is logged by the service as proof the user authorised the remote signing transaction.

Responsive to Encryption Uplift Needs : If an encryption mechanism is suddenly undermined having a centrally controlled service which can quickly adopt a new more secure mechanism reduces organisational risk

Easy Integration : The authorised remote signing solution can be utilized by any health care provider application by making OAuth2 based REST API calls to the Service signing engine.

**NHS Identity understands the importance of offering these benefits to our users and has **prioritised** to deliver this capability in its future road map.**
