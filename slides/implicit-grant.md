### Implicit Grant

![](images/implicit.png)

---

## Implicit Grant

An implicit authorization grant is similar to an authorization code grant, except the access token is returned to the client application already after the user has finished the authorization.

The access token is thus returned when the user agent is redirected to the redirect URI.

---

## Implicit Grant

This of course means that the access token is accessible in the user agent, or native application participating in the implicit authorization grant.

The access token is not stored securely on a web server.

---

## Implicit Grant

Furthermore, the client application can only send its client ID to the authorization server.

If the client were to send its client secret too, the client secret would have to be stored in the user agent or native application too.

That would make it vulnerable to hacking.

---

## Implicit Grant

Implicit authorization grant is mostly used in a user agent or native client application.

The user agent or native application would receive the access token from the authorization server.
