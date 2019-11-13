# CORS 
## Same Origin Policy (SOP)

According to Wikipedia

> Under Same-origin policy (SOP), a web browser permits scripts contained in a first web page to access data in a second web page, but only if both web pages have the same origin

SOP made sure, we can only make call to same origin from where the JS file is downloaded using **XMLHttpRequest** and **fetch**

## Why Same Origin Policy is important

Lets assume for a minute, there is no Same Origin Policy

We are somehow tricked into visiting www.safehdfcbank.com. On that site, there is an iframe that loads www.hdfc.com, where you proceed to login legitimately.

After logging in, a simple JavaScript call from www.safehdfcbank.com could be used to access the DOM elements of www.hdfc.com loaded in the iframe, such as your account number, balance etc

Same Origin Policy prevents us from above vulnerability

## When two URLs are considered same origin ?

Origin = URI scheme(http or https) + host name + port number

Lets say our host is http://www.hdfc.com

| URL from which we try to access 	| Accessible | Reason |
| --- 								| ---------- | ------ |
| http://www.hdfc.com/home 			|  Yes  | Protocol, host and port match |
| http://www.hdfc.com/dir2/other.htm | Yes | Protocol, host and port match |
| http://www.hdfc.com:81/home | No | port mismatch |
| https://www.hdfc.com | No | Schema mismatch (https) |
| http://www.demo.hdfc.com | No | Host mismatch |
| http://www2.hdfc.com | No | Host mismatch |


## JSONP

When a JS is downloaded from an origin, it can't make access content from another origin. But a webpage can load download using `<script src=""/>` JS from another origin & execute it

This loophole is used as way to bypass the SOP. See the below example (taken from Wikipedia)

Lets say call to http://example.com/Users/1234 will yield the following JSON

```
{
    "Name": "Foo",
    "Id": 1234,
    "Rank": 7
}
```

We can't directly call this URL like below

```
<script type="application/javascript"
        src="http://example.com/Users/1234">
</script>
```

which will result in error as JS will consider the JSON as data block & hence will throw syntax error.

Instead the call will be made to third party to return response like below

<script src="http://example.com/Users/1234?callback=parseResponse"></script>

Now the third party service has to respond with creating a JS file with below content

`parseResponse({"Name": "Foo", "Id": 1234, "Rank": 7});`

Once a JS file is downloaded, browser as usual will execute it (whenever a JS file gets downloaded, browser will try to execute it). Hence the parseResponse() method already written in our JS will get called with JSON as the parameter

This method of bypassing SOP is called **JSONP** (JSON Padding)

## Cross Origin Resource Sharing (CORS)

> Cross-origin resource sharing (CORS) is a mechanism that enables scripts running on a browser to interact with resources from a different origin

CORS allow access other origin resource by adding **additional headers**. CORS specifies two types of request such as Simple Request & Preflight Request

### Simple Request

A request is called as Simple Request, if it satisies all the below conditions

* Allowed HTTP Methods : GET, POST, or HEAD
* Allowed HTTP Headers : Accept, Accept-Language, Content-Language, Last-Event-ID, Content-Type
* Allowed Content Type : application/x-www-form-urlencoded, multipart/form-data, or text/plain

### CORS for Simple Request

When a simple request is made to different Origin, CORS will do the following

* Browser will make request to the resource (URL) of different origin (server)

```
GET Users/1234?callback=parseResponse HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:71.0) Gecko/20100101 Firefox/71.0
Accept: application/json
Connection: keep-alive
Origin: http://www.vicky.com
```
* Server will process the call & respond back with JSON & an additional header called **Access-Control-Allow-Origin**

```
HTTP/1.1 200 OK
Date: Thu, 14 Nov 2019 00:00:00 GMT
Access-Control-Allow-Origin: http://www.vicky.com
Content-Type: application/json

{
    "Name": "Foo",
    "Id": 1234,
    "Rank": 7
}
```
If **Access-Control-Allow-Origin** header matches with host URL, the browser will allow the JS to access the response. Otherwise browser will thrown an error


Other Access-Control headers - Access-Control-Allow-Methods, Access-Control-Allow-Headers, Access-Control-Max-Age

**Note**: For simple request, the cross origin server didn't block any request. It sends the response with an additional header. Its the browser which blocks the code from accessing the response received from cross origin server

### CORS for Preflight or Not-so-simple-request

If a request does not meet the criteria for a simple request, the browser will instead make an automatic preflight request using the OPTIONS method

```
OPTIONS /
Host: example.com
Origin: http://www.vicky.com
```

Response from browser for **Options** request

```
Access-Control-Allow-Origin: http://www.vicky.com
Access-Control-Allow-Methods: PUT, DELETE
```

Based on the response for the OPTIONS request, browser will decide whether to continue with the request or to abandon it

Here is the workflow of CORS (Image from Wikipedia)

![CORS Explained in one Image - Source: Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Flowchart_showing_Simple_and_Preflight_XHR.svg/770px-Flowchart_showing_Simple_and_Preflight_XHR.svg.png)







 
