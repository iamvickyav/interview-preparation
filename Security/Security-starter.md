# Encryption & Decryption

** Notes prepared from "Sunny Classroom" Youtube channel

## Private-Key Encryption

- Data is encrypted & decrypted using same key
- Symmetric key Encryption

### Methods of Private-Key Encryption

1. Stream Ciphers
2. Block Ciphers

### Stream Cipher

Encrypts single bit at a time

E.g RC4 - Rivest Cipher 4

### Block Cipher

Encrypts data in block (certain length). Data comes as chunk  

Size is usually 64, 128 or 256 bits

E.g DES, AES, IDEA

## Private-Key Encryption

- Two different keys (Public & Private key) to encrypt and decrypt data
- Keys are mathematically related
- Asymmetric key Encryption
- Public key is public to anyone. Private key is private to creator of these keys
- Data is encrypted with public key & decrypted with private key
- Receiver creates the pubic & private key

**Issues**

- Can't verify the sender because public key is public
- To prove sender authenticity, they use digital signature

## Digital Signature

- Electronic verification of the sender
    - **Authentication** of sender
    - **Non-Repudiation** Integrity Message not altered in transit
    - **Sender** can't deny sending msg later

- Bob wants to send something to Alice
    - Bob created public & private key
    - Bob shares public key to Alice
    - Bob hashes his plain text message using some hashing algo & then encrypts the message using his private key. This is called the digital signature
    - Bob sends the message to Alice
    - Alice uses Bob's public key to decrypt Bob's digital signature
    - If decryption successful, then sender's integrity is authenticated
    - On decryption, Alice gets the hash. She already has the plain text message sent by Bob
    - She hashes the plain text with same hashing algo & if the resultant hash & hash he got from Bob are same. Message is not tampered in transit
    
Note : Message is sent in plain text & hacker may change entire message in transit

## Digital Certificates

- Electronic credentials issued by third party
- Based on trust, because we rely on third party (CA) which issues the certificate

- Notary lawyer sign in bond ensures all other signature are legitimate

## SSL

- HTTP over SSL (Secure Socket Layer)  is HTTPS
- SSL cert - Issued by 3rd party CA, verifies identity of server & its public key

### How it works

- Hit a HTTPS page from browser
- Server respond with its public key + Digital Certificate (issued by 3rd party CA)
   
    Digital Signature
   - Created by CA's private key
   - Browser's by default have many CA's public key
- On receiving SSL cert, browser validates it against CA
- Browser creates one symmetric key
- Uses Webserver's public key to encrypt the symmetric key. Sends it to server
- On receiving it webserver will decrypt the message using its private key
- Now any communication between client & webserver is encrypted using symmetric key

Hence

- HTTPS uses public & private key combination
- public key to verify the server's identity & its public key
- private key to send data between them
- Latest is SSL 3.0

## SSL/TLS 

- TLS is upgraded version of SSL
- TLS v1.1 & v1.2 available