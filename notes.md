
Auth0 and okta are Identity providers
OAuth = Security protocal

OAuth flow components:
 - Client App - eg. profile management webapp
 - resource owner - Customer
 - Identity provider - Auth0
 - Resource server - eg. Customer Profile Service API

refer: https://auth0.com/docs/authorization/protocols/protocol-oauth2

OAuth 2.0 uses two endpoints: the `/authorize` endpoint and the `/oauth/token` endpoint.

OAuth grant: a way to receive token

Flows:
 - Implicit Grant
 - Authorisation code grant
 etc.,

 #### OAuth is an authorization protocal(what you are allowed to do) not for authentication(who you are)

 OpenID Connect is used for authentication:

 three layers:
    HTTP -> OAuth 2.0 -> OpenId connect


OIDC - used for authentication using identity token JWT
OAuth - used for authorisation using access token (can be JWT or just string) contains scopes eg. `read:products`

The most common authentication protocols are SAML2p, WS-Federation and OpenID Connect – SAML2p being the most popular and the most widely deployed.

OpenID Connect is the newest of the three, but is considered to be the future because it has the most potential for modern applications. It was built for mobile application scenarios right from the start and is designed to be API friendly.

IdentityServer is middleware that adds the spec compliant OpenID Connect and OAuth 2.0 endpoints to an arbitrary ASP.NET Core application.

#### Identity Token
An identity token represents the outcome of an authentication process. It contains at a bare minimum an identifier for the user (called the sub aka subject claim) and information about how and when the user authenticated. It can contain additional identity data.

#### Access Token
An access token allows access to an API resource. Clients request access tokens and forward them to the API. Access tokens contain information about the client and the user (if present). APIs use that information to authorize access to their data.


- It is recommended to use Implicit flow for client side rendered webapps and authorisation code flow for native mobile apps.

3 login flows for Auth0 - Universal(lock widget hosted by auth0), Embedded(lock widget embeded) and CustomUI

Allowed callback url had to be updated while creating a new application in Auth0

