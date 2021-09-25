# What is OAuth

Auth does not reveal password information, instead relying on authorization tokens to establish a connection between users and service providers. OAuth is a security mechanism that allows you to authorize one application to engage with another on your behalf without disclosing your password.

## Give an example of what using OAuth would look like.

time we wish to log in with a new account, similar to how we log into Netlify using GitHub.

## How does OAuth work? What are the steps that it takes to authenticate the user?

OAuth is not authentication. It's an authorization protocol, or, better yet, a delegation protocol. It's for this reason that identity protocols such as OpenID Connect
exist and legacy protocols such as SAML use extension grants to link authentication and delegation.

## What is OpenID?

OpenID allows you to use an existing account to sign in to multiple websites, without needing to create new passwords

## What is the difference between authorization and authentication?

In simple terms, it's like giving someone official permission to do something or anything. For example, the process of verifying and confirming employees ID and passwords in an organization is called authentication, but determining which employee has access to which floor is called authorization.

## What is Authorization Code Flow with Proof Key for Code Exchange (PKCE)?

![img](https://res.cloudinary.com/practicaldev/image/fetch/s--nD5yBd8s--/c_imagga_scale,f_auto,fl_progressive,h_720,q_auto,w_1280/https://cdn-images-1.medium.com/max/1600/1%2A3CxVf-0jG5GWBGew3lingQ.png)

The Authorization Code Flow + PKCE is an OpenId Connect flow specifically designed to authenticate native or mobile application users.

## What is Client Credentials Flow?

In the client credentials flow, permissions are granted directly to the application itself by an administrator. When the app presents a token to a resource, the resource enforces that the app itself has authorization to perform an action since there is no user involved in the authentication.

![img1](https://membrane-soa.org/images/oauth2/flows/credentials/01.png)
## What is Resource Owner Password Flow?

The Resource Owner Password Credentials flow allows exchanging the username and password of a user for an access token and, optionally, a refresh token. ... The primary difference is that the user's password is accessible to the application. This requires strong trust of the application by the user.

![img](https://docs.wso2.com/download/attachments/60493894/OAuth%20grant%20types%20-%20password.png?version=1&modificationDate=1510604129000&api=v2)
