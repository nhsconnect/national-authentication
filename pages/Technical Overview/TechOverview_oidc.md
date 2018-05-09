---
title: An Overview of OpenID Connect
keywords: explore, design, reference
sidebar: overview_sidebar
permalink: TechOverview_oidc.html
summary: An introduction to the main concepts of OpenID Connect.
---

## Introduction

OpenID Connect 1.0 is a simple identity layer on top of the OAuth 2.0 protocol. It allows Clients to verify the identity of an End-User based on the authentication performed by an authorisation server, as well as to obtain basic profile information about the End-User in an interoperable and REST-like manner.

OpenID Connect allows clients of all types, including Web-based, mobile, and JavaScript clients, to request and receive information about authenticated sessions and end-users. The specification suite is extensible, allowing participants to use optional features such as encryption of identity data, discovery of OpenID Providers and session management.

The full set of specifications describing OpenID Connect can be found at <http://openid.net/connect/>.

## Authentication Flow Types

OpenID Connect defines three types of authentication flow to cater for different client types: the authorisation Code Flow, the Implicit Flow and the Hybrid Flow. These are briefly described below with the authorisation Code Flow being described in more detail [here](explore_auth_code_flow).

#### Authorisation Code Flow

This is the most commonly used flow and is used with web applications as well as native applications that utilise a client/server architecture. In this flow rather than return the id, access and refresh Tokens directly to the Relying Party's client component an authorisation code is returned. The Relying Party's server component can then exchange the code for the required tokens. This provides the dual benefits of:

1. Not exposing any tokens to the user agent or applications with access to the user agent.
2. Allowing the Relying Party to be authenticated before exchanging the code for tokens.

This flow requires that a Relying Party can securely maintain a client secret between themselves and the OpenID Provider.

#### Implicit Flow

The Implicit Flow is mainly used by Relying Parties implemented as a client in a browser using a scripting language or as a native application that does not utilise a client/server architecture. In this flow tokens are returned directly to the client. This is a less secure mechanism as this may may expose the tokens to the End-User or applications that have access to the user agent. In this flow the OpenID Provider does not authenticate the Relying Party.

#### Hybrid Flow

This is a rarely used flow that allows the Relying Party's client and server components to receive tokens separately from one another. Essentially it is a combination of the code and implicit flows.


   
## High Level Process Flow

The diagram below depicts at a a high level the OpenID Connect authentication process.

![OpenID Connect High Level Flow](images/OIDCHighLevelFlow.jpg)


### Open ID Process Flow Description



| Step| Description|
| ----- | --------- |
|1|The Relying Party sends a request to the OpenID Provider to authenticate the End-User. The request must include the Relying Party’s identity and the openid scope, it may optionally include other scopes e.g. the email scope if the Relying Party wishes to obtain the user’s email address.|
|2|The OpenID Provider authenticates the End-User using one of the methods available to it and obtains authorisation from the End-user to provide the requested scopes to the identified Relying Party.|
|3|Once the End-User has been authenticated and has authorised the request the OpenID Provider will respond to the Relying Parting with an id token identifying the End-User and optionally with access and refresh tokens granting access to the userinfo endpoint.|
|4|Optionally the Relying Party may request the additional user information (e.g. email address) from the userinfo endpoint by presenting the access token obtained in the previous step.|




The above gives a generic flow however there are three variations of this flow as described above.


