# REST
(Notes based on book - Hands-On RESTful API Design Patterns and Best Practices)

* REST stands for REpresentational State Transfer
* Architectural style & not a programming language or technology
* In REST, everything is a Resource
* Resources are identified using URI
* Resources can be delivered in any representation - JSON, XML, Image etc. They are also called as Multipurpose Internet Mail Extension (MIME) types

## Constraints in REST

One has to follow allow below constraints to get declared as RESTful

#### Client-server
    
The communication happens through request-response pattern. Hence we need a protocol for communication to happen seemlessly.
    
RESTful APIs should use HTTP (Stateless Protocol)

---

#### Statelessness

Each request has to be independent meaning client has to send information on every request to server
   
Helps achieve scalability

---
    
#### Cacheable

Ability to store frequently accessed data
    
**Different Caches** - Browser caches, proxy caches, gateway caches (reverse-proxy)
    
**Controlling Cache Behaviour using headers** - Expires, Cache-Control, E-Tag, Last-modified

**Advantages** - Reduced bandwidth, latency (response time), load on server

---

#### Uniform interface

URI + HTTP Methods

URL is an URI

---

#### Layered systems

A client should not know whether it is connected to the services directly with the server endpoint, or to an intermediary before reaching the actual server

---

#### Code on demand

Server can send code to the clients to be executed on the client computer

Only one optional constraint of REST

**E.g.** Java Applets, Flash

---

## In Depth

### URI Syntax

- Forward slash (/) separator - represent hierarchy
- Avoid trailing forward slash 
    
    E.g. http://www.google.com/mail/ (avoid / at last)
- Use Hyphens but not Underscores in URI
- Keep everything in lowercase in URI

---

### Resource Archetypes

- Document, Collection, Store, and Controller

#### Document
Object instance or a database record

Use singular nouns for document names

---

#### Collection
Collection of resource

Use plural nouns for collections

Managed by Server

Client can propose a change in the collection which server can accept/reject

URI is decided by server

```
E.g. https://finance.india.gov.in/gst-forms
```
---

#### Store
Client-managed resource repository

Client have full edit access

URI chosen by client

Use plural nouns for stores

```
E.g. https://www.youtube.com/playlist/illayara-songs
```
---

#### Controller
To perform application-specific actions

Use verb to represent action

---

## Security

### Same domain policy

Restrictions imposed by the web browsers for JavaScript client

Prevents JS Client from accessing resources if the JS & Resource are not from same domain

---

#### Resource Sharing
If you want JS Client from other domains to access your endpoint, use either of below method

- JSON with padding (JSONP)
- CORS

---

## Other topics to read

### RMM

Richardson Maturity Model (RMM)

### HATEOAS

HATEOAS means an application state representation (resource) that includes links to related resources

