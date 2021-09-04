
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




