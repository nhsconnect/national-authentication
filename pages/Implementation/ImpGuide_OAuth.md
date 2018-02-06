---
title: Implementing Authorization -  OAuth 2.0
keywords: explore, design, reference
sidebar: overview_sidebar
permalink: ImpGuide_OAuth.html
summary: A detailed description of the NHS Digital implementation of Authorisation - OAuth 2.0.
---

{% include warning.html content="*NEEDS SIGNIFICANT RE-WRITING AND SIMPLIFYING - Currently in draft format" %}



## Introduction ##

Authorisation is granting the relevant access right to the client based on RBAC.
The user must be authenticated before executing the Authorisation operations. 
The prerequisite for executing the Authorisation operations are:
> * **Authorisation Code**
> * **ID Token**

---

## Authorisation Request (Access Token Request)
### Description
When an `authorisation code` (using code or hybrid flow) has been obtained, a `token` request can be made to get the `access token`.
### Protocol Example
The diagram below shows the content of the authorisation request type
![Authorisation Request](images/AuthorisationRequestTypev1.JPG)



The client directs the resource owner to the constructed URI using an HTTP redirection response, or by other means available to it via theuser-agent.

For example, the client directs the user-agent to make the following HTTP request using TLS (with extra line breaks for display purposes only):
```sh
    GET /authorize?
	    response_type=code&
		client_id=s6BhdRkqt3&
		&scope=openid%20profile%20email
		state=xyz&
		redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
    Host: server.example.com
```

### Python Coding Example
```sh
TokenRequest tokenReq = new TokenRequest(
  providerMetadata.getTokenEndpointURI(),
  new ClientSecretBasic(clientInformation.getID(),
                        clientInformation.getSecret()),
  new AuthorizationCodeGrant(authCode, redirectURI));

HTTPResponse tokenHTTPResp = null;
try {
  tokenHTTPResp = tokenReq.toHTTPRequest().send();
} catch (SerializeException | IOException e) {
  // TODO proper error handling
}

// Parse and check response
TokenResponse tokenResponse = null;
try {
  tokenResponse = OIDCTokenResponseParser.parse(tokenHTTPResp);
} catch (ParseException e) {
  // TODO proper error handling
}

if (tokenResponse instanceof TokenErrorResponse) {
  ErrorObject error = ((TokenErrorResponse) tokenResponse).getErrorObject();
  // TODO error handling
}

OIDCAccessTokenResponse accessTokenResponse = (OIDCAccessTokenResponse) tokenResponse;
accessTokenResponse.getAccessToken();
accessTokenResponse.getIDToken();
```

### Supporting Information 

On successful execution of the above request the outcome will be an [access token](TechOverview_Artefacts.html#access-token-example-jwt).

----

## Request Additional Information  (User Information Request)

### Description
Using the access token, information about the end user can be obtained by making a user info request:
### Protocol Example

The diagram below shows the sample content of the userInfo request

![User Information Claim Additional Information ](images/UserInfoRequest.JPG)

Additional claims can be requested such as `date of birth`, `address`, `gemder` and many more. For claim attributes can be viewed on the [OPENID Connect specification](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims)
Any information about the user can be requested as specified in Open ID Connect Specification

### Python Coding Example
```sh
from oic.oic.message import ClaimsRequest, Claims
# setup claims to get email, phone number, 1st name and surname
claims_request = ClaimsRequest(
    id_token=Claims(
      email={"essential": None},
      phone_number=None
    ),
    userinfo=Claims(
      given_name={"essential": True},
      family_name={"essential": True}, nickname=None
    )
)
# set arguments directing a claims request
request_args = {
    "redirect_uri": "https://example.com/rp/authz_cb",
    "scope": "openid",
    "response_type": "code",
    "claims": claims_request
}

# client is oic.oic.Client
client.construct_AuthorizationRequest(request_args=request_args)
```

### Supporting Information 

Specific claims can be requested using the Authorization request parameter







