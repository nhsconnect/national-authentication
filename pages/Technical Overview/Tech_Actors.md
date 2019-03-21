---
title: Actors 
keywords: homepage
sidebar: overview_sidebar
permalink: Tech_Actors.html
toc: true
summary: A brief introduction to the Actors involved in the Authentication and Authorisation.
---

## Introduction

---

This section will define the actors used during the Authentication and Authorisation Service.  These will be used throughout this section and in the detailed NHS implmentation Guide.

## Actor List


![Actor List ](images/Actor list-Jekyll.jpg)




## Actor Responsibility Summary

| Actor | Description |
| ------ | -------------|
| Client | An application making protected resource requests on behalf of the resource owner and with its authorisation.  The term "client" does  not imply any particular implementation characteristics (e.g., whether the application executes on a server, a desktop, or other devices).This is sometimes known as the Relying Party |
| Relying Party | The client application requesting End-User authentication and information about the End-User. This can also be referred to as a Client. |
| Authentication Server | The server issuing access tokens to the client after successfully authenticating the resource owner and obtaining authorisation.  An OAuth 2.0 Authorisation Server that is capable of authenticating an End-User and providing information to a Relying Party about the authentication event and the End-User. This is also refered as an OpenID Provider(OP) |
| Resource Owner | An entity capable of granting access to a protected resource.When the resource owner is a person, it is referred to as an end-user. |
| Resource Server | The server hosting the protected resources, capable of accepting and responding to protected resource requests using access tokens. |
| End-User| The human participant being authenticated and about whom the Relying Party is requesting information.|
| UserInfo Endpoint | An OAuth 2.0 Protected Resource that returns Claims about the authenticated End-User. |
| Token Endpoint | The endpoint where a relying party(client) obtains an Access Token, ID Token and optionally a refresh token from. |