# Learn about Certificates

**Certificates are all about machine identity**

An X.509 certificate is a digital certificate that uses the widely accepted international X.509 public key infrastructure (PKI) standard to verify that a public key belongs to the user, computer or service identity contained within the certificate.

**Against malicious network impersonators**

With algorithms like RSA, we can do following things with private/public key

* Encrypt
* Decrypt
* Sign
* Verify

Above 4 things are used for authentication

CA is a self signed cert but added in list of authorized CAs in the computer

PRIVATE KEY -> Sign & PUBLIC KEY -> Verify
PRIAVTE KEY -> DECRYPT & PUBLIC KEY -> ENCRYPT

One person can sign & every can verify
Everyone can encrypt with public key but only one with private key can decrypt

Its not impossible to figure the private key if you have the public key. But just that it would just take incredibly long time. So we can consider **cypher is computationally secure**

So to use certificate for authentication, we need
* Certificate
* Private key
* Public key (stored inside the certificate)

Lets Encrypt -> Free Open Source CA. Provides Certificate after authenticating proof of control over a DNS domain

Provides Certificate & Private Key

When you have control over both client & server, you can use self signed certs
