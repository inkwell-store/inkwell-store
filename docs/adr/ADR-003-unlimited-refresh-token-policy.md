# Unlimitd refresh token policy

## Context
In the OAuth framework, a **client** might ask an **authorization server** for an access token, which in turn can be used by the former to access resources from a **resource server**. Access tokens should be short-lived, so the window for exploitation is also short (a couple of minutes).

Once an access token expires the client might use a **refresh token** to request a new one. These tokens, issued by the authorization-server, are sent alongside access tokens and are long-lived, with hours, to days or even weeks in some cases.

One issue that emerges from this setup is how many refreshes can be done with a single refresh token until it's revoked?

## Options considered
1. One refresh token can ask for one access token. At which point the authorization server must revoke the current refresh token and return a new one.
2. One refresh token can ask for a limited number of access tokens. Once this threshold is met the refresh token is revoked and the authorization server must generate a new one.
3. One refresh token can ask for any amount of access tokens within its life spam or until it's revoked.

## Decision
I choose **option (3)** because it makes storing both the refresh and access tokens much simpler. The refresh_token can be stored locally using a secure http-only cookie which cannot be read with javascript. This implementation is enough for what the application realisticly needs, without implementing deep securiy measures, especially the ones regarding refresh token policies from OAuth2.1.

The overhead and complexity for this time is not worth it. With this implementation one client might receive a set of access and refresh tokens and only a single refresh token exists at any time inside the client. This means that only a single refresh token can be associated with a client at any time, and, when it expires or gets revoked manually it can be safely discared for a new (single) refresh token. With this strategy managing such credentials become substantialy easier, because the authorization server doesn't need to constantly emit new refresh tokens, nor do I need to evaluate a quota for a single refresh token. Naturaly, these features will make the application more secure and they might be implemented in the future, but not right now.

## Consequences
* If somehow an attacker captures the refresh token they will have access to an unlimited refresh attempts.
* Implementing refresh token rotations and/or families is still possible even with this approach.