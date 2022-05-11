# Securing REST Endpoints

> To understand basics of REST, read [REST STARTER Guide](https://github.com/iamvickyav/interview-preparation/blob/master/Concepts/REST-Starter.md) 


Since HTTP is stateless, its necessary to attach client related (session)information in every HTTP request. 

But the question is where to keep the client related information ?

Lets say, we keep the client related information in Server (Probably in DB), then we need to use sessions

## Using Session

When user logs in, servers generate a random session token which
points to the actual session data in the database and sends it back to the client

The client has to attach this session token to every future request

On receiving the token, server will make a DB call to verify the token & get client related information

This approach needs additional DB calls everytime. Hence slow

## JWT

Use JWT Tokens where the user information stored in Token itself

### Format

```
<header>.<payload>.<signature>
```

Anyone can read header & payload section by decoding a JWT token (check the example at [jwt.io](https://jwt.io/))

But there is protection against tampering of token. The signature part is encrypted & key is known only to Server. On receiving the token, server validates the token to ensure no tampering is made on token

### Header

```
{
  "alg": "RS256",
  "typ": "JWT"
}
```

Algo can be either none (unsecure), HS256 or RS256

#### HS256 

HS256 is hash function & needs a password (key) which is stored in server alone. 

* Hash functions can be brute forced. 
* Encryprtion & Decryption neeeds same key. Hence password has to be shared between Authentication server & Application server

Hence RS256 is preferred 

#### RS256

RS256 uses two keys for encryption & decryption

* Authentication server (the one which generates JWT) uses private key to sign JWT
* Application server will use public key to validate the JWT 
* RSA encryption is relatively slow compared to a hashing function

> Attacker wants to forge JWT, not validate. So Public Keys can be shared across

[Above details about JWT headers are taken from here](https://blog.angular-university.io/angular-jwt/)

### Payload 

Payload contains registered claims, public & private claims

**Registered Claim Names** - iss (issuer), exp (expiration time), sub (subject), aud (audience)

**Public claims**

https://www.iana.org/assignments/jwt/jwt.xhtml

On further request, client sends the Authorization header with Bearer

```
Authorization: Bearer <token>
```

### Issues with JWT

* Expiry is embedded in token, hence hard to revoke/
invalidate

E.g. taken from [JSON Web Tokens (JWTs) Are Not Safe](https://redis.com/wp-content/uploads/2022/03/jwts-not-safe-e-book.pdf) document from Redis

> Imagine you logged out from Twitter after sending your tweet. You’d think that you are logged out of the server, but that’s not the case because JWT is self-contained and will continue to work until it expires

* Posssibility of [Replay Attack](https://www.geeksforgeeks.org/replay-attack/). HTTPS is necessary to avoid eaves dropping

