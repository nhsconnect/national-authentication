---
title: Implementing Authentication -  OpenID Connect
keywords: explore, design, reference
sidebar: overview_sidebar
permalink: ImpGuide_OIDC.html
summary: A detailed description of the NHS Digital implementation of Authentication OpenID Connect.
---

## Introduction

Authentication involves the identification of the users claim: proving who the user is before the Authorisation Service is initated.  

The following artefacts are a product of a successful Authentication Service

> * **Authorisation Code**
> * **ID token (if the client doesn’t have one)**
  
This section provides an example of implementing key operations within the Authentication Service using Java and Python; languages that are predominantly used in NHS Digital DDC.

[//]:# (In this section we will walk through the various requests and response messages relating to Authenticaltion and Authorisation with example code.)

---
## Authentication Request
### Description
The authentication request is done by redirecting the end user to the provider, for more details see the OIDC specification. The redirect URL is built as follows, using the Authorization Code Flow.

### Protocol Example

The diagram below shows the content of the `Authentication Request`:

![Authentication Request Type](images/AuthenticationRequestType.JPG)

There are more parameters defined by the [OpenId Connect Specification](http://openid.net/specs/openid-connect-core-1_0.html#AuthRequest)


```sh 
GET /authorize?
    response_type=code%20id_token
    &client_id=s6BhdRkqt3
    &redirect_uri=https%3A%2F%2Fclient.example.org%2Fcb
    &scope=openid%20profile%20email
    &nonce=n-0S6_WzA2Mj
    &state=af0ifjsldkj HTTP/1.1
  Host: server.example.com
```

### Python Coding Example
```sh
# Instantiate the client
from oic.oic import Client
from oic.utils.authn.client import CLIENT_AUTHN_METHOD

client = Client(client_authn_method=CLIENT_AUTHN_METHOD)

# out of band static setup of provider
from oic.oic.message import ProviderConfigurationResponse

op_info = ProviderConfigurationResponse(
    version="1.0", issuer="https://example.org/OP/1",
    authorization_endpoint="https://example.org/OP/1/authz",
    token_endpoint="https://example.org/OP/1/token",
    ... and so on )

# or
# op_info = ProviderConfigurationResponse(**info)
# if you have the provider info in the form of a dictionary

client.provider_info = op_info


# statically set client info
from oic.oic.message import RegistrationResponse
# set client id and secret
info = {"client_id": "1234567890", "client_secret": "abcdefghijklmnop"}
client_reg = RegistrationResponse(**info)

client.store_registration_info(client_reg) m oic import rndstr
from oic.utils.http_util import Redirect

# setup session and nonce
session["state"] = rndstr()
session["nonce"] = rndstr()
# set openid connect arguments 
args = {
    "client_id": client.client_id,
    "response_type": "code",
    "scope": ["openid"],
    "nonce": session["nonce"],
    "redirect_uri": client_uri,
    "state": session["state"]
}
# Setup the auth request
auth_req = client.construct_AuthorizationRequest(request_args=args)
# execute request
login_url = auth_req.request(client.authorization_endpoint)
# redirect to the login url
return Redirect(login_url)
```	

### Supporting Information
In this example there is only one  identityprovider so the authorization endpoint URL received as part of a out-of-band manual registration process has been read into client.authorization_endpoint.
The CAS Service  provider does not support dynamic client registration, so again  the client id has been received out-of-band and read from configuration into the variable client_uri.
Make sure `redirectURI` matches a URI known by the provider.
The `state` and nonce should be stored so they can be retrieved later.

---





## Authorisation Code
### Description
The authentication response is sent from the provider by redirecting the end user to the redirect URI specified in the initial authentication request from the client. 
The Authorization Code can be extracted from the query part of the redirect URL:


### Protocol Example
```sh
HTTP/1.1 302 Found
  Location: https://client.example.org/cb#
    code=SplxlOBeZQQYbYS6WxSbIA
    &id_token=eyJ0 ... NiJ9.eyJ1c ... I6IjIifX0.DeWt4Qu ... ZXso
    &state=af0ifjsldkj
```	





### Python Coding Example
```sh
from oic.oic.message import AuthorizationResponse

# If you're in a WSGI environment
response = environ["QUERY_STRING"]
# receive the response
aresp = client.parse_response(AuthorizationResponse, info=response,
                              sformat="urlencoded")
# set the authorization code 
code = aresp["code"]
# check the state is as expected
assert aresp["state"] == session["state"]

```	


### Supporting Information
The above example is the authorization code client.

When using either implicit or hybrid flow the authentication response is encoded in the fragment part of the URL. This requires additional handling, e.g. using Javascript
aresp is an instance of an AuthorizationResponse or an ErrorResponse. The latter if an error was returned from the OP. Among other things you should get back in the authentication response is the same state value as you used when sending the request.


---

## ID Token Request

### Description
The ID token resembles the concept of an identity card, in a standard JWT format, signed by the OpenID Provider (OP). To obtain one the client needs to send the user to their OP with an authentication request.

### Protocol Example

The diagram below shows the content of the `ID Token Request`:

![ID token Request Type](images/IDTokenRequest.JPG)

```json
POST /token HTTP/1.1
	Host: server.example.com
	Content-Type: application/x-www-form-urlencoded
	Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
		grant_type=authorization_code
		&code=SplxlOBeZQQYbYS6WxSbIA
		&redirect_uri=https%3A%2F%2Fclient.example.org%2Fcb
```	

### Python Coding Example

```sh
# set the arguments to the returned authorisation code
args = {
    "code": aresp["code"]
}
# perform the token request
resp = client.do_access_token_request(state=aresp["state"],
                                      request_args=args,
                                      authn_method="client_secret_basic")
# userinfo will be set to ‘openid’ information
userinfo = client.do_user_info_request(state=aresp["state"])
```	

### Supporting Information

When an authorization code (using code or hybrid flow) has been obtained, a token request can be made to get the access token and the id token ‘scope’ has to be the same as in the authentication request.

If you don’t specify a specific client authentication method, then client_secret_basic is used.

The response you get back is an instance of an AccessTokenResponse or again possibly an ErrorResponse instance.

If it’s an AccessTokenResponse the information in the response will be stored in the client instance with state as the key for future use. One of the items in the response will be the ID Token which contains information about the authentication. One parameter (or claim as it is also called) is the nonce you provide with the authentication request.

 Using the state, the client library will find the appropriate access token and based on the token type choose the authentication method.

