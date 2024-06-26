# Video References

- [OAuth 2.0 and OpenID Connect (in plain English)](https://www.youtube.com/watch?v=996OiexHze0 "OAuth 2.0 and OpenID Connect (in plain English)") (this is the best one, also the longest)
- [How to Hack OAuth](https://www.youtube.com/watch?v=aU9RsE4fcRM "How to Hack OAuth")
- [An Illustrated Guide to OAuth and OpenID Connect](https://www.youtube.com/watch?v=t18YB3xDfXI "An Illustrated Guide to OAuth and OpenID Connect")
- [Vulnerabilities of mobile OAuth 2.0 by Nikita Stupin, Mail.ru](https://www.youtube.com/watch?v=vjCF_O6aZIg&ab_channel=scrt.insomnihack) (there's a topic on PKCE here)

# Identity Use Cases

| Case                    | Type           | Implementation |
| ----------------------- | -------------- | -------------- |
| Simple login            | Authentication | oidc           |
| SSO                     | Authentication | oidc           |
| Mobile login            | Authentication | oidc           |
| Delegated authorization | Authorization  | OAuth 2.0      |

# OAuth 2.0 Flow

![[Pasted image 20230304032400.png]]

# Oidc Flow
![[Pasted image 20230304032424.png]]
>Note that scope now includes openid and authorization server sends back an ID token as well

RFCs

- [RFC-6749 The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749)
- [RFC-7009 OAuth 2.0 Token Revocation](https://datatracker.ietf.org/doc/html/rfc7009)
- [RFC-7519 JSON Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519)
- [RFC-7662 OAuth 2.0 Token Introspection](https://datatracker.ietf.org/doc/html/rfc7662)
- [RFC-9068 JWT Profile for OAuth 2.0 Access Tokens](https://datatracker.ietf.org/doc/html/rfc9068#name-validating-jwt-access-token)