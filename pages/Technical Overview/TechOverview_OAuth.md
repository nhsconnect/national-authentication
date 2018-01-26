---
title: The Authorization Code Flow in Detail
keywords: explore, design, reference
sidebar: overview_sidebar
permalink: TechOverview_OAuth.html
summary: A detailed description of the Authorization Code Flow.
---

## Introduction

The Authorization Code Flow is the most commonly used variant of the OpenID Connect authentication flows. It is suited for use with web applications and native applications that utilise a client/server architecture. In this flow rather than return the id, access and refresh tokens directly to the Relying Party's client component an authorization code is returned. The Relying Party's server component can then exchange the code for the required tokens.

This provides the dual benefits of:

1. Not exposing any tokens to the user agent or applications with access to the user agent.
2. Allowing the Relying Party to be authenticated before exchanging the code for tokens.

This flow requires that a Relying Party can securely maintain a client secret between themselves and the OpenID Provider.

## High Level Flow

The diagram below depicts at a a high level the Authorization Code Flow.

![Authorization Code Flow](images/OIDCAuthCodeFlow.jpg)

### Authorisation Code Flow Description

| Step| Description|
| ----- | --------- |
|1|The Relying Party sends a request to the OpenID Provider to authenticate the End-User. The request must include the Relying Party’s identity and the openid scope, it may optionally include other scopes e.g. the email scope if the Relying Party wishes to obtain the user’s email address.|
|2|The OpenID Provider authenticates the End-User using one of the methods available to it and obtains authorization from the End-user to provide the requested scopes to the identified Relying Party.|
|3|Once the End-User has been authenticated and has authorized the request the OpenID Provider will return an authorization code to the Relying Party’s server component.|
|4|The Relying Party’s server component contacts the token endpoint and exchanges the authorization code for an id token identifying the End-User and optionally access and refresh tokens granting access to the userinfo endpoint.|
|4|Optionally the Relying Party may request the additional user information (e.g. email address) from the userInfo endpoint by presenting the access token obtained in the previous step.|

This flow is described in much more detail in the Implemntation Guide sections.
