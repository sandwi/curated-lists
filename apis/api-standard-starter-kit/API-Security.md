# API Security
# Protect API using OAuth2
[OAuth2](https://oauth.net/2/) is standard mechanism to protect REST APIs. OAuth2 offers 4 types of flows called Authorization Grant Types to protect APIs.  

## OAuth2 Grant Type Decision Logic
This section assumes familiarity with OAuth2.0 grant types. If not, please review [OAuth2 Grant Types](https://oauth.net/2/grant-types/) and [RFC6749](https://tools.ietf.org/html/rfc6749#section-1.3) section 1.3 on Authorization Grant.

An OAuth2.0 grant is a method of acquiring an access token. Deciding which grants to implement depends on the type of client the end-user will be using, and the experience that is desired for end-users. Figure below shows the decision logic for selecting which grant type to use based on the client.

![](https://github.com/sandwi/curated-lists/blob/master/apis/oauth2-grant-type-decision-logic.png)

**First party or third party client?**

A first party client is a client that we trust enough to handle the end user’s authorization credentials. For example iPhone & Android apps are developed and owned by a company, therefore these can be implicitly trusted.

A third party client is a client that we don’t trust i.e. apps not developed by the company. These apps are developed by partners or other providers, and can be native apps or single page web apps.

**Access Token Owner?**

An access token represents a permission granted to a client to access a protected resource.

If we are authorizing a machine to access resources then we don’t require the permission of a user to access said resources, we should implement the [client credentials grant](https://tools.ietf.org/html/rfc6749#section-1.3.4).

If we require the permission of a user to access resources we need to determine the client type.

**Client Type?**

Depending on whether or not the client is capable of keeping a secret will depend on which grant the client should use.

If the client is a web application that has a server side component then we should implement the [authorization code grant(https://tools.ietf.org/html/rfc6749#section-1.3.1).

Although for a client that is a single page web application i.e. it runs entirely on the front end, we can implement the [implicit grant](https://tools.ietf.org/html/rfc6749#section-1.3.2) but strongly recommend using implement the [authorization code grant(https://tools.ietf.org/html/rfc6749#section-1.3.1) instead.

If the client is a native application such as a mobile app we should implement the [password grant](https://tools.ietf.org/html/rfc6749#section-1.3.3).

Third party native applications should use the [authorization code grant](https://oauth2.thephpleague.com/authorization-server/auth-code-grant/) (via the native browser, not an embedded browser - e.g. for iOS push the user to Safari or use [SFSafariViewController](https://developer.apple.com/library/ios/documentation/SafariServices/Reference/SFSafariViewController_Ref/), don't use an embedded [WKWebView](https://developer.apple.com/library/ios/documentation/WebKit/Reference/WKWebView_Ref/)).

# Entitlements or Granular Permissions
OAuth2 Authorization Servers don't implement Entitlements (aka granular permissions) for users. Entitlement interpretation and validation capabilities are specific to a service, hence these are implemented by the service or via an Entitlement Service. OAuth2 provides facilities for implementing granular permissions using "aud" (audience), "scope" and other custom claims that can be included in the JWT. But interpretation and enforcement is service specific. 
