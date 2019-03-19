---
title: Introduction to Authentication types
keywords: homepage
sidebar: overview_sidebar
permalink: AuthenType_Intro.html
toc: true
summary: A brief introduction to the Authentication types offered by NHS identity.
---
To satisfy the requirements of a given Authenticator Assurance level (AAL), a claimant SHALL be authenticated with at least a given level of strength to be recognized as a subscriber. The result of an authentication process is an identifier that SHALL be used each time that subscriber authenticates to that Relying Party (RP). Subscriber identifiers SHOULD NOT be reused for a different subject but SHOULD be reused when a previously-enrolled subject is re-enrolled by the Credential service Provider (CSP). Other attributes that identify the subscriber as a unique subject MAY also be provided. 
The NHS Identity provides several authentication options that can be leveraged depending on the needs of the client users.

**AAL1:** AAL1 provides some assurance that the claimant controls an authenticator bound to the subscriber’s account. AAL1 requires either single-factor or multi-factor authentication using a wide range of available authentication technologies. Successful authentication requires that the claimant prove possession and control of the authenticator through a secure authentication protocol.

**NHS Identity’s AAL1 authentication supports the following authenticator types:** 
> * Memorized Secret.
> * Single-Factor One-Time Password (OTP) Device.

The other Authentication types suggested by the NIST guidelines are:
> * Out-of-Band Devices.
> * Look-Up Secret.
> * Multi-Factor OTP Device.
> * Single-Factor Cryptographic Software.
> * Single-Factor Cryptographic Device. 
> * Multi-Factor Cryptographic Software.
> * Multi-Factor Cryptographic Device.

**AAL2:** AAL2 provides high confidence that the claimant controls authenticator(s) bound to the subscriber’s account. Proof of possession and control of two distinct authentication factors is required through secure authentication protocol(s). Approved cryptographic techniques are required at AAL2 and above.

At AAL2, authentication SHALL occur using either a multi-factor authenticator or a combination of two single-factor authenticators. A multi-factor authenticator requires two factors to execute a single authentication event, such as a cryptographically-secure device with an integrated biometric sensor that is required to activate the device.

When a multi-factor authenticator is used, the National Institute of Standards & Technology (NIST) suggests using any of the following:
> * Multi-Factor OTP Device.
> * Multi-Factor Cryptographic Software.
> * Multi-Factor Cryptographic Device.

When a combination of two single-factor authenticators are used, it SHALL include a Memorized Secret authenticator and one possession-based (i.e., “something you have”) authenticator from the following list:

> * Look-Up Secret.
> * Out-of-Band Device.
> * Single-Factor OTP Device. 
> * Single-Factor Cryptographic Software.
> * Single-Factor Cryptographic Device.

**NHS Identity currently supports a combination of two single-factor authenticators that include a Memorized Secret (i.e.,” something you know”) and a Single-Factor OTP Device (i.e., “something you have”).**

**AAL3:** AAL3 provides very high confidence that the claimant controls authenticator(s) bound to the subscriber’s account. Authentication at AAL3 is based on proof of possession of a key through a cryptographic protocol. AAL3 authentication SHALL use a hardware-based authenticator and an authenticator that provides verifier impersonation resistance; the same device MAY fulfil both these requirements. To authenticate at AAL3, claimants SHALL prove possession and control of two distinct authentication factors through secure authentication protocol(s). Approved cryptographic techniques are required.

NIST suggests that AAL3 authentication SHALL occur using one of a combination of authenticators:

> * Multi-Factor Cryptographic Device. 
> * Single-Factor Cryptographic Device used in conjunction with Memorized Secret.
> * Multi-Factor OTP device (software or hardware) used in conjunction with a Single-Factor Cryptographic Device.
> * Multi-Factor OTP device (hardware only) used in conjunction with a Single-Factor Cryptographic Software.
> * Single-Factor OTP device (hardware only) used in conjunction with a Multi-Factor Cryptographic Software Authenticator.
> * Single-Factor OTP device (hardware only) used in conjunction with a Single-Factor Cryptographic Software Authenticator and a Memorized Secret.

**NHS Identity would be supporting AAL3 Authentication using Apple Ipads from April 2019. This mechanism would meet the Multi-Factor Cryptographic Device guidelines. FIDO2 would be the next supported authentication mechanism which would be available by Q3 of 2019.**