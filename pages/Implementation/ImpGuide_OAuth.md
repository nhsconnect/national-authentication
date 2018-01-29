---
title: Implementing Authorization -  OAuth 2.0
keywords: explore, design, reference
sidebar: overview_sidebar
permalink: ImpGuide_OAuth.html
summary: A detailed description of the NHS Digital implementation of Authorisation - OAuth 2.0.
---
Will be removed in final
{% include warning.html content="The implementation details for the offline use case as described below may change in future versions." %}

## Introduction

Authorisation is granting the relevant access right to the client based on RBAC.
The user must be authenticated before executing the Authorisation operations. 
The prerequisite for executing the Authorisation operations are:
> * **Authorisation Code**
> * **ID Token**

### Authorisation Request

|**Description**|The id token obtained from the token request must be validated, see  OpenID connect for ID token validation.|
|**Protocol Example**| ..|
|**Coding Example**| [Java Example](ImpGuide_Author_Req_Java.html),  Python click here |
|**Supporting Information**| ..|

### Request Additional Information (User Info Request)

|**Description**|Using the access token, information about the end user can be obtained by making a user info request|
|**Protocol Example**| ..|
|**Coding Example**| [Java Example](ImpGuide_UserInfo_Req_Java.html),  Python click here |
|**Supporting Information**| ..|




