---
layout: post
published: false
title: Mining Social Media with Python  (1)
subtitle: Set Up Twitter API Authentications
date: '2017-07-31'
categories:
  - Data Mining
  - Social Media Intelligence
tags:
  - Python
---

Twitter uses [OAuth](https://oauth.net/) to provide authorized access to its API. OAuth is an open protocol to allow **secure** authorization in a **standard** method from web, mobile and desktop applications. 

Twitter API Authentication Model
There are two forms of authentication.

User authentication
This is the most common form of resource authentication in Twitter’s OAuth 1.0a implementation. A signed request identifies an application’s identity in addition to the identity accompanying granted permissions of the end-user the application is making API calls on behalf of, represented by the user’s access token.

Application-only authentication
Application-only authentication is a form of authentication where an application makes API requests on its own behalf, without a user context. API calls are still rate limited per API method, but the pool each method draws from belongs to the entire application at large, rather than from a per-user limit. API methods that support this form of authentication will contain two rate limits in their documentation, one that is per user (for application-user authentication) and the other is per app (for this form of application-only authentication). Not all API methods support application-only authentication, because some methods require a user context (for example, a Tweet can only be created by a logged-in user, so user context is required for that operation).


## References
* [Twitter's OAuth Documentation](https://dev.twitter.com/oauth)
* [OAuth](https://oauth.net/)