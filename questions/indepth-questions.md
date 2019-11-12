1. Difference between PUT & POST
2. What is UTF -8?
3. What is CORS ?

WEB-INF directory so there can be no direct access by clients

RestTemplate is a synchronous client to perform HTTP requests

WebClient is a non-blocking, reactive client to make HTTP request, introduced in Spring 5.0


HTTP Versus WebSocket

In HTTP and REST, an application is modeled as many URLs. To interact with the application, clients access those URLs, request-response style. Servers route requests to the appropriate handler based on the HTTP URL, method, and headers

By contrast, in WebSockets, there is usually only one URL for the initial connect. Subsequently, all application messages flow on that same TCP connection. This points to an entirely different asynchronous, event-driven, messaging architecture

WebSocket is also a low-level transport protocol, which, unlike HTTP, does not prescribe any semantics to the content of messages. That means that there is no way to route or process a message unless the client and the server agree on message semantics