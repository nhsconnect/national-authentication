---
title: ASP.net (C#) Example, Client
keywords: homepage
sidebar: overview_sidebar
permalink: ImpGuide_ASPExample.html
toc: true
summary:  ASP.net (c#) Example.
---


## Introduction
 


The following example shows the how to authenticate a user from an ASP.Net web application and to get some claims information about that user.
Four steps are involved in getting going from scratch:
> 1.	You need VS 2017 and ASP.Net Core Framework set up on your computer. 
> 2.	Create your basic ASP.NET Core application as a starting point
> 3.	Modify your application to defer authentication to the CAS Service.
	
### Create your basic ASP.NET Core web application
To create you new web site just create a new project in VS 2017 and choose the ASP.NET Core Web Application



|<img src="./images/ASPNET1.JPG" alt="ASPnet"/>|

Next you just pick Web Application with no authentication.


|<img src="./images/ASPNET2.JPG" alt="ASPnet"/>|

Next get the [Microsoft Middleware OpenID Connect packages](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect/)

Open the NPM Package Manager Console to install the packages:

```sh
# Pull down the new packages
install-package Microsoft.AspNetCore.Authentication.Cookies
install-package Microsoft.AspNetCore.Authentication.OpenIdConnect
install-package Microsoft.AspNetCore.Authentication.JwtBearer
```

This will add the needed packages, and you may rebuild once the package restore process has completed.

Next add the initialization code to the Startup class (in `Startup.cs`):

```sh
// Import the relevant namespaces at the top of the file
using System.IdentityModel.Tokens.Jwt;
using Microsoft.AspNetCore.Authentication.OpenIdConnect;
```

In the `Configuration` method add these lines after the `app.UseStaticFiles();` line. .

```sh
app.UseCookieAuthentication(new CookieAuthenticationOptions {
    AuthenticationScheme = "Cookies",
    AutomaticAuthenticate = true
});

var options = new OpenIdConnectOptions() {
    AuthenticationScheme = "oidc", // callback will be on /signin-oidc
    SignInScheme = "Cookies",
    ResponseType = "code",
    Authority = YOUR_DOMAIN, // e.g.: "https://cas.nhs.uk.nationalid"
    ClientId = YOUR_CLIENT_ID, // e.g  "urn:casid:aspnet-core-demo" 
    ClientSecret = YOUR_CLIENT_SECRET //e.g."0m4bGC+LO7QSBk7zf4d2Uhhlq48IRHbUC/D5yM4EROU="
};

// This may be modified to get the choice of authentication method from
// some other source, e.g. a dropdown in the UI
// NOT NEEDED??? for most OIDC identity proivders, such as Google, etc.
options.Events = new OpenIdConnectEvents() {
    OnRedirectToIdentityProvider = context => {
        context.ProtocolMessage.AcrValues = "urn:????????????????";
        return Task.FromResult(0);
    }
};

// Wire in OIDC middelware
app.UseOpenIdConnectAuthentication(options);

```

The `options` object sets the OpenID Connect middelware behaviour.

Specifically the `authorisationScheme` property determines the callback you must register with your OpenID Connect identity provider (see the section at the end on how to do that for easyID). In this case we set it to `oidc` which means the callback will be on/`signin-oidc`. Still, this is handled by the middelware so no need for any additional code.
We are now ready to authenticate. Before trying it out we just need a protected resource that will display user information.

### The protected view: Start the login and show the user info

First add a login link to the front page. Put a login link in the menu, or something to the same effect, in the `_Layout.cshtml` shared view where the top menu is rendered:


```sh
@if (Context.User.Identity.IsAuthenticated) 
{
    <li><a asp-area="" asp-controller="Home" asp-action="Logout">Logout</a></li>                        
}
else 
{
    <li><a asp-area="" asp-controller="Home" asp-action="Protected">Login</a></li>                        
}

```

To implement the `Protected` view which will kick off the authentication process, add a new action to the `HomeController`. Notice the `Authorise` attribute which will start the OIDC flow.

```sh
// The Authorise attribute requires the user to be authenticated and will
// kick off the OIDC authentication flow 
[Microsoft.AspNetCore.Authorisation.Authorise]
public IActionResult Protected()
{
    return View();
}
    
public async Task<IActionResult> Logout()
{
    await HttpContext.Authentication.SignOutAsync("Cookies");
    return View("Index");
}

```

Now, adding a simple view, `Protected.cshtml`, in the `Views/Home` to display the claims, and we are set.

```sh
@{
    ViewData["Title"] = "ASP.NET Core + NationalNHSID";
}
<h2>Welcome @User.Claims.Where( c => c.Type == "name").FirstOrDefault().Value</h2>
 
<dl>
    @foreach (var claim in User.Claims)
    {
        <dt>@claim.Type</dt>
        <dd>@claim.Value</dd>
    }
</dl>
```
## Running the application

To execute an a login flow, remember to set the `authorisation`, the `ClientID`, and the `ClientSecret`. 
If you haven’t already set up an CAS ID account, go to [Here](ImpGuide_Reg.html) to do that.

Hit F5 and you’re off. Once the front page has opened up click the Login menu at the top.
