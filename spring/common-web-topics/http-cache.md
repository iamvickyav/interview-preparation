# Cache in HTTP

Caching is a technique that stores a copy of a given resource and serves it back when requested

Advantage - reduce latency & traffic

Removing from Cache is called Eviction, Cache before expiration time is called fresh, Cache after expiry is called stale

### Summary about Cache

* Different kinds of caches - private (browser), shared/proxy caches (ISP level), gateway (CDN)

* Perfect for Cache - 200 (OK), 301 (Moved Permanently), 404 (Not Found)

* HTTPS won’t be cached by shared caches

* Cache is fresh (server without checking server) if expiry time set, and is still within the fresh period. A request for a stale resource will be forwarded with If-None-Match to check if it is in fact still fresh. If so, the server returns a 304 (Not Modified)

* If stale, the origin server will be asked to validate it. It won't be evicted or ignored

* Under certain circumstances — for example, when it’s disconnected from a network — a cache can serve stale responses without checking with the origin server

### How to check freshness

* If "Cache-control: max-age=N" header available, then the freshness = N
* If max-age not present, check for expires. If present then value of expires - date header
* If neither of them present, look for a Last-Modified header

## Cache-Control 

The Cache-control header for defining cache policy

|Cache Control Header Value | Usage |
| ------------------------- | ----- |
| Cache-Control: no-store   | Don't Cache |
| Cache-Control: no-cache   | Cache but revalidate |
| Cache-Control: private    | can be stored in browser |
| Cache-Control: public		 | can be stored anywhere |
| Cache-Control: max-age=seconds |  max time a resource will be considered fresh |
| Cache-Control: s-maxage		  | similar to max-age but only for shared |
| Cache-Control: must-revalidate | expired ones should not be used |
| Cache-Control: proxy-revalidate| similar to must revalidate but only for shared |
| Cache-Control: stale-while-revalidate | can use the current (stale) version while it re-fetches the latest version in the background |
| Cache-Control: stale-if-error| use stale is refetch fails |


If both Cache-Control and Expires present, Cache-Control takes precedence

### Cache validation

If Cache-control: must-revalidate present or If the Cache is expired

ETag - response header - opaque-to-the-useragent - strong validator

If ETag present, the client can issue an If-None-Match in the header of future requests to validate the cached resource

Last-Modified response header - a weak validator - if present client can issue an If-Modified-Since request header to validate the cached document

On validation, server can response with a normal 200 OK, or it can return 304 Not Modified (with an empty body)

### Best practices

* If Cache implemented, page visit stats may get affected. To solve it use 1x1 transparent uncacheable image for every page


![Cache Explained in one Image - Source: Google](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/images/http-cache-decision-tree.png)

Reference:

https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching

https://jakearchibald.com/2016/caching-best-practices/

https://www.mnot.net/cache_docs/

https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching



