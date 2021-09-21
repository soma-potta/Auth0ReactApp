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

This project uses auth0.js sdk for interactions with Auth0:

Setup Auth0 session:

```
import auth0 from 'auth0-js';

auth0 = new auth0.WebAuth({
            domain: REACT_APP_AUTH0_DOMAIN,
            clientID: REACT_APP_AUTH0_CLIENTID,
            redirectUri: REACT_APP_AUTH0_CALLBACK_URL,
            responseType: "token id_token",
            scope: "openid profile email"
        });
```

Logout:  
If logout is requested on server, then all the SSO applications will be logged out. Prior setup callback redirect url in Auth0 dashboard.

```
auth0.logout({
    clientID: process.env.REACT_APP_AUTH0_CLIENT_ID,
    returnTo: "http://localhost:3000"
})
```

Reading user profile:

```
auth0.client.userInfo( accessToken, (err, profile) => {

});
```

API calls:

- Create an API in Auth0 with name and identifier. Auth0 generates an Id.

- Add Audience, identifier of the api to the client call. So auth0 generates a token for the specified audience.

```
import auth0 from 'auth0-js';

auth0 = new auth0.WebAuth({
            domain: REACT_APP_AUTH0_DOMAIN,
            clientID: REACT_APP_AUTH0_CLIENTID,
            redirectUri: REACT_APP_AUTH0_CALLBACK_URL,
            audience: REACT_APP_AUTH0_AUDIENCE
            responseType: "token id_token",
            scope: "openid profile email"
        });
```

verfiying JWT is two steps:

1. Verifiy signature
2. Verify claims(exp - expiration date, iss - Issuer, aud - Audience)

OAuth Scopes:
https://auth0.com/docs/configure/apis/scopes

Scopes are added to API in auth0

Rules:
Customize default auth flow.
e.g. Email verification

Rule can be created by javascript functions.

Authorisation options:

1. Scope - Scopes were designed to specify what an application is allowed to do with a third party on a user's behalf. If custom scopes were used for authorization it may lead to bloated jwts. Not scalable for complex scenarios.
   e.g. Users can delete only the products they created.

2. Roles - this is simple, secure and scalable. Roles can be added to jwt.
   Note: Use scopes when interacting with thrid parties and use roles for handling your app's permissions.

3. Session cookies - identifies the user and the resource server makes database calls to identify the user privileges on the resource. It means it only does authentication not authorization.

ref: https://app.pluralsight.com/library/courses/react-auth0-authentication-security/table-of-contents
