---
title: Data Artefacts, ID & Access Token
keywords: homepage
sidebar: overview_sidebar
permalink: TechOverview_Artefacts.html
toc: true
summary: An overview of the key Artefact used for Authentication and Authorisation.
---

{% include important.html content="*NEEDS SIGNIFICANT RE-WRITING AND SIMPLIFYING BASED ON Token TA discussion*" %}


## Introduction

This section describes in more detail some of the data artefacts used in the `Open ID` and `OAuth 2.0` flows.  

The two tokens produced for the Care Access Service are summarised below

![ID Access Token](images/IDAccessTokenv1.JPG)

|Token| Description|
|---|---|
|ID Token| A JSON Web Token (JWT) that contains claims about the `authentication` event and may contain claims about the End-User. An ID Token is requested using the openid scope and thus is used during the `authentication` service. |
|Access Token| An `access tokens` is a credential used to access protected resources. It represents specific scopes and durations of access, granted by the resource owner, and enforced by the resource server and `authorisation`.  OAuth 2.0 supports a number of access token types, the type used by OpenID Connect are bearer tokens which can be simply understood as meaning "give access to the bearer of this token". Access tokens can have different formats, structures, and methods of utilization based on the resource server security requirements. However they are represented as a string the structure of which is usually opaque to the client.|






## ID Token

The diagram below shows the content of an ID Token

![ Key Artefacts ](images/IDTokenContent.JPG)

As a minimum the ID token will contain the following claims:

|Claim|Name|Cardinality| Description|
|-----|----|-----------|----|
|iss|Issuer Identifier| Mandatory|An identifier for OpenID Provider.|
|sub|Subject Identifier| Mandatory|A unique identifier for the End-User.|
|aud|Audience(s)| Mandatory|The identifier of the Relying Party and any other parties intended as a recipient.|
|exp|Expiration|Mandatory |The time on or after which the ID Token must not be accepted for processing.|
|iat|Issuance Time| Mandatory|The time at which the JWT was issued.|
|auth_time|Authentication Time| Optional|Time when the End-User authentication occured|
|nonce|...|Optional |String value used to associate a Client session with an ID Token, and to mitigate replay attacks. |
|acr|Authentication Context Class reference|Optional |Shows the level of assurance|
|amr|Authentication Method Reference|Optional |This shows the authentication methods used in the authentication, eg One Time Password, Push Notification, Certificates etc|
|azp|Authorised party|Optional |The party to which the ID token was issued. If present, it MUST contain the OAuth 2.0 Client ID of this party. This Claim is only needed when the ID Token has a single audience value and that audience is different than the authorized party. It MAY be included even when the authorized party is the same as the sole audience. The azp value is a case sensitive string containing a StringOrURI value. |




 

The **ID Token** may additionally contain other claims:

> 1. OpenID Connect defines a number of optional claims that may be returned depending on the flow being used and the parameters provided in the initial request. For example a Relying Party may supply a nonce parameter in the original request and this will be returned unmodified in a nonce claim to allow the Relying Party to mitigate against a replay attack.
>
> 2. Additionally an OpenID Provider implementation may optionally decide to return additional user information in the ID Token e.g. a name claim containing the End-User's full name or a SpineRoles claim containing  a users clinical spine access.

For more details see the [OpenID Connect Core Specification](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) for a standard set of claims.


The `ID Token` is a JSON Web Token ([JWT](https://tools.ietf.org/html/rfc7519)) that contains claims about the **Authentication** of an End-User and their **Identity**. It may optionally contain other data about the End-User.

The claims are represented in a simple JSON object as shown in the example below.

### ID Token Payload Example 

```
{
 "iss": "https://server.example.com",
 "sub": "24400320",
 "aud": "s6BhdRkqt3",
 "nonce": "n-0S6_WzA2Mj",
 "exp": 1311281970,
 "iat": 1311280970,
 "auth_time": 1311280969,
 "acr": "urn:mace:incommon:iap:silver"
 "amr": ["mfa", "pwd","otp"]
}
```


### ID Token Example (JWT)

The JSON object is signed using a JSON Web Signature [JWS](https://tools.ietf.org/html/rfc7515) and optionally may be encrypted using JSON Web Encryption [JWE](https://tools.ietf.org/html/rfc7516). Signing the token allows the integrity and origin of the token to be validated by the Relying Party whilst encrypting the token provides confidentiality.

Finally the id token header, JSON claims and signature are encoded into a Base64URL strings separated by a . character e.g.

```
"eyJhbGciOiJSUzI1NiIsImtpZCI6IjFlOWdkazcifQ.ewogImlzc
yI6ICJodHRwOi8vc2VydmVyLmV4YW1wbGUuY29tIiwKICJzdWIiOiAiMjQ4Mjg5
NzYxMDAxIiwKICJhdWQiOiAiczZCaGRSa3F0MyIsCiAibm9uY2UiOiAibi0wUzZ
fV3pBMk1qIiwKICJleHAiOiAxMzExMjgxOTcwLAogImlhdCI6IDEzMTEyODA5Nz
AKfQ.ggW8hZ1EuVLuxNuuIJKX_V8a_OMXzR0EHR9R6jgdqrOOF4daGU96Sr_P6q
Jp6IcmD3HP99Obi1PRs-cwh3LO-p146waJ8IhehcwL7F09JdijmBqkvPeB2T9CJ
NqeGpe-gccMg4vfKjkM8FcGvnzZUN4_KSP0aAp1tOJ1zZwgjxqGByKHiOtX7Tpd
QyHE5lcMiKPXfEIQILVq0pc_E2DzL7emopWoaoZTF_m0_N0YzFC6g6EJbOEoRoS
K5hoDalrcvRYLSrQAZZKflyuVCyixEoV9GfNQC3_osjzw2PAithfubEEBLuVVk4
XUVrWOLrLl0nx7RkKU8NXNHq-rvKMzqg"
```

---



## Access Token 

The diagram below shows the content of an Access Token

![ Key Artefacts ](images/AccessTokenContent.JPG)

As a minimum the Access token will contain the following claims:




|Claim|Name|Cardinality |Description|
|----|-----|-----|----|
|iss|Issuer Identifier|Mandatory |Requesting systems issuer URI. For tokens issued by the national authentication solution, this will be the URL of that national service. For tokens issued by a different issuer, this will hold the URL for the issuer. |
|sub|Subject Identifier|Mandatory|A unique identifier for the End-User.  An identifier for the person or system that has been authorised for access. In most cases this will be an identifier for a member of staff, identified by a Spine URP ID (see RBAC) for details|
|aud|Audience(s)|Mandatory|The identifier of the Relying Party and any other parties intended as a recipient, e.g. API endpoint URL. The URI for the API Endpoint. This will be the fully qualified endpoint address returned to the Consumer by the SDS endpoint lookup service as the value of `nhsMhsEndPoint`. |
|exp|Expiration|Mandatory|The time on or after which the Access Token must not be accepted for processing.|
|iat|Issuance Time|Mandatory|The time at which the JWT was issued.|
|reason_for_request|n/a | | Purpose for which access is being requested. This is currently limited to one of the following values: `directcare`, `secondaryuses` or `patientaccess`.|
|requested_scope|n/a | | Data being requested:  This is a space-separated list of the scopes authorised for this user. Individual APIs will check this list to establish whether the authorisation grants access to the data being request by the client, and will reject the call if the appropriate scopes have not been granted in the token.  |
|requesting_system |n/a |n/a | Identifier for the system or device making the request.  This is an identifier for the deployed client system that has been authorised to make API calls. In the case of Spine-enabled clients (or those using the SSP to broker API calls), this will be a Spine Accredited System ID (ASID). The naming system prefix for the ASID will be `https://fhir.nhs.uk/Id/accredited-system` |
|requesting_organization |n/a |Optional| Organisation making the request.  This is the ODS code of the care organisation from where the request originates.The naming system prefix for the ODS code will be `https://fhir.nhs.uk/Id/ods-organization-code`|
|requesting_user |n/a |Optional|Health or Social Care professional making the request |



### Access Token Payload Example ###

```json
{
	"iss": "https://cas.nhs.uk",
	"sub": "https://fhir.nhs.uk/Id/sds-role-profile-id"|[SDSRoleProfileID]",
	"aud": "https://provider.thirdparty.nhs.uk/GP0001/STU3/1",
	"exp": 1469436987,
	"iat": 1469436687,
	"reason_for_request": "directcare",
	"requested_scope": "patient/*.read",
	"requesting_system": "https://fhir.nhs.uk/Id/accredited-system|[ASID]",
	"requesting_organization": "https://fhir.nhs.uk/Id/ods-organization-code|[ODSCode]",
	"requesting_user": "https://fhir.nhs.uk/Id/sds-role-profile-id"|[SDSRoleProfileID]"
}
```



### Access Token Example (JWT)

The final output is three `Base64url` encoded strings separated by dots (note - there is some canonicalisation done to the JSON before it is `Base64ur`l encoded, which the JWT code libraries will do for you).

```shell
eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJpc3MiOiJodHRwOi8vZWMyLTU0LTE5NC0xMDktMTg0LmV1LXdlc3QtMS5jb21wdXRlLmFtYXpvbmF3cy5jb20vIy9zZWFyY2giLCJzdWIiOiIxIiwiYXVkIjoiaHR0cHM6Ly9hdXRob3JpemUuZmhpci5uaHMubmV0L3Rva2VuIiwiZXhwIjoxNDgxMjUyMjc1LCJpYXQiOjE0ODA5NTIyNzUsInJlYXNvbl9mb3JfcmVxdWVzdCI6ImRpcmVjdGNhcmUiLCJyZXF1ZXN0ZWRfcmVjb3JkIjp7InJlc291cmNlVHlwZSI6IlBhdGllbnQiLCJpZGVudGlmaWVyIjpbeyJzeXN0ZW0iOiJodHRwOi8vZmhpci5uaHMubmV0L0lkL25ocy1udW1iZXIiLCJ2YWx1ZSI6IjkwMDAwMDAwMzMifV19LCJyZXF1ZXN0ZWRfc2NvcGUiOiJwYXRpZW50LyoucmVhZCIsInJlcXVlc3RpbmdfZGV2aWNlIjp7InJlc291cmNlVHlwZSI6IkRldmljZSIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6IldlYiBJbnRlcmZhY2UiLCJ2YWx1ZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn1dLCJtb2RlbCI6IkRlbW9uc3RyYXRvciIsInZlcnNpb24iOiIxLjAifSwicmVxdWVzdGluZ19vcmdhbml6YXRpb24iOnsicmVzb3VyY2VUeXBlIjoiT3JnYW5pemF0aW9uIiwiaWQiOiIxIiwiaWRlbnRpZmllciI6W3sic3lzdGVtIjoiaHR0cDovL2ZoaXIubmhzLm5ldC9JZC9vZHMtb3JnYW5pemF0aW9uLWNvZGUiLCJ2YWx1ZSI6IltPRFNDb2RlXSJ9XSwibmFtZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn0sInJlcXVlc3RpbmdfcHJhY3RpdGlvbmVyIjp7InJlc291cmNlVHlwZSI6IlByYWN0aXRpb25lciIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6Imh0dHA6Ly9maGlyLm5ocy5uZXQvc2RzLXVzZXItaWQiLCJ2YWx1ZSI6IkcxMzU3OTEzNSJ9LHsic3lzdGVtIjoibG9jYWxTeXN0ZW0iLCJ2YWx1ZSI6IjEifV0sIm5hbWUiOnsiZmFtaWx5IjpbIkRlbW9uc3RyYXRvciJdLCJnaXZlbiI6WyJHUENvbm5lY3QiXSwicHJlZml4IjpbIk1yIl19fX0.
```









### Refresh Token

A refresh token is a credential used to obtain access tokens.  Refresh tokens are issued to the client by the authorization server and are  used to obtain a new access token when the current one becomes invalid or expires, or to obtain additional access tokens with identical or narrower scope.

Unlike access tokens, refresh tokens are intended for use only with authorization servers and are never sent to resource servers. 

As for access tokens a refresh token is represented as a string that is usually opaque to the client e.g. 

```
refresh_token=9yNOxJtZa5
```  
   
### UserInfo

As described above the id token principally holds claims about the authentication event and the identity of the End-User. A Relying Party  wishing to obtain further data about the End-User can do this by presenting the access token they obtained to the userinfo endpoint.

A successful request will result in a JSON object containing claims about the End-User being returned. As a minimum this will always contain the sub claim which the Relying Party must verify to protect against a token substitution attack.

An example JSON object is given below:

```json
  {
   "sub": "248289761001",
   "name": "Jane Doe",
   "given_name": "Jane",
   "family_name": "Doe",
   "preferred_username": "j.doe",
   "email": "janedoe@example.com",
  }
```


