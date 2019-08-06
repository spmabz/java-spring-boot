### HTTP is simple
HTTP is generally designed to be simple and human readable. HTTP messages can be read and understood by humans, providing easier developer testing, and reduced complexity for new-comers.

### HTTP is extensible: 
New functionality can even be introduced, by a simple agreement between a client and a server about a new header's semantics.

### HTTP is stateless, but not sessionless:
HTTP is stateless: there is no link between two requests being successively carried out on the same connection, or not. This immediately becomes problematic when users wanted to interact with a page in a coherent way, for example with an e-commerce shopping basket. Using header extensibility, HTTP Cookies are added to the workflow, allowing session creation on each HTTP request to share the same context or the same state.

While the core of HTTP itself is stateless, HTTP cookies allow the use of stateful sessions.

### HTTP and connections:
A connection is controlled at the transport layer, and therefore fundamentally out of scope for HTTP. Though HTTP doesn't require the underlying transport protocol to be connection-based; only requiring it to be reliable, or not loose messages (so at minimum presenting an error). Among the two most common transport protocols on the Internet, TCP is reliable and UDP isn't. HTTP subsequently relies on the TCP standard, which is connection-based, even though a connection is not always required.

HTTP/1.0 opened a TCP connection for each request/response exchange, introducing two major flaws: opening a connection needs several round-trips of messages and therefore slow, but becomes more efficient when several messages are sent, and regularly sent: warm connections are more efficient than cold ones.

In order to mitigate these flaws, HTTP/1.1 introduced pipelining (which proved difficult to implement) and persistent connections: the underlying TCP connection can be partially controlled using the Connection header. HTTP/2 went a step further by multiplexing messages over a single connection, helping keep the connection warm, and more efficient.

### What can be controlled by HTTP
This extensible nature of HTTP has, over time, allowed for more control and functionality of the Web. Cache or authentication methods were functions handled early in HTTP history. The ability to relax the origin constraint, by contrast, has only been added in the 2010s.

Here is a list of common features controllable with HTTP.

- **Cache:**
How documents are cached can be controlled by HTTP. The server can instruct proxies, and clients, what to cache and for how long. The client can instruct intermediate cache proxies to ignore the stored document.
- **Relaxing the origin constraint:**
To prevent snooping and other privacy invasions, Web browsers enforce strict separation between Web sites. Only pages from the same origin can access all the information of a Web page. Though such constraint is a burden to the server, so HTTP headers can relax this strict separation server-side, allowing a document to become a patchwork of information sourced from different domains (there could even be security-related reasons to do so).
- **Authentication:**
Some pages may be protected so only specific users can access it. Basic authentication may be provided by HTTP, either using the Authenticate and similar headers, or by setting a specific session using HTTP cookies.
- **Proxy and tunneling:**
Servers and/or clients are often located on intranets and hide their true IP address to others. HTTP requests then go through proxies to cross this network barrier. Not all proxies are HTTP proxies. The SOCKS protocol, for example, operates at a lower level. Others, like ftp, can be handled by these proxies.
- **Sessions:**
Using HTTP cookies allows you to link requests with the state of the server. This creates sessions, despite basic HTTP being a state-less protocol. This is useful not only for e-commerce shopping baskets, but also for any site allowing user configuration of the output.

## URL

### Scheme or protocol

![](images/mdn-url-protocol@x2.png)

`http://` is the protocol. It indicates which protocol the browser must use. Usually it is the HTTP protocol or its secured version, HTTPS. The Web requires one of these two, but browsers also know how to handle other protocols such as mailto: (to open a mail client) or ftp: to handle file transfer, so don't be surprised if you see such protocols.

 Common schemes are:

|Scheme|	Description|
|---|---|
|data|	Data URIs|
|file|	Host-specific file names|
|ftp|	File Transfer Protocol|
|http/https|	Hyper text transfer protocol (Secure)|
|mailto|	Electronic mail address|
|ssh|	Secure shell|
|tel|	telephone|
|urn|	Uniform Resource Names|
|view-source|	Source code of the resource|
|ws/wss|	(Encrypted) WebSocket connections|

### Authority

![](images/mdn-url-domain@x2.png)

`www.example.com` is the domain name or authority that governs the namespace. It indicates which Web server is being requested. Alternatively, it is possible to directly use an IP address, but because it is less convenient, it is not often used on the Web.

### Port
![](images/mdn-url-port@x2.png)


`:80` is the port in this instance. It indicates the technical "gate" used to access the resources on the web server. It is usually omitted if the web server uses the standard ports of the HTTP protocol (80 for HTTP and 443 for HTTPS) to grant access to its resources. Otherwise it is mandatory.

### Path
![](images/mdn-url-path@x2.png)

`/path/to/myfile.html` is the path to the resource on the Web server. In the early days of the Web, a path like this represented a physical file location on the Web server. Nowadays, it is mostly an abstraction handled by Web servers without any physical reality.

### Query string
![](images/mdn-url-parameters@x2.png)

`?key1=value1&key2=value2` are extra parameters provided to the Web server. Those parameters are a list of key/value pairs separated with the & symbol. The Web server can use those parameters to do extra stuff before returning the resource to the user. Each Web server has its own rules regarding parameters, and the only reliable way to know how a specific Web server is handling parameters is by asking the Web server owner.

## HTTP Messages

HTTP messages are composed of textual information encoded in ASCII, and span over multiple lines. In HTTP/1.1, and earlier versions of the protocol, these messages were openly sent across the connection. 

HTTP requests, and responses, share similar structure and are composed of:

1. A start-line describing the requests to be implemented, or its status of whether successful or a failure. This start-line is always a single line.
An optional set of HTTP headers specifying the request, or describing the body included in the message.
1. A blank line indicating all meta-information for the request have been sent.
1. An optional body containing data associated with the request (like content of an HTML form), or the document associated with a response. The presence of the body and its size is specified by the start-line and HTTP headers.
1. The start-line and HTTP headers of the HTTP message are collectively known as the head of the requests, whereas its payload is known as the body.

![](images/HTTPMsgStructure2.png)

## HTTP Requests

![](images/HTTP_Request_Headers2.png)

Bodies can be broadly divided into two categories:

- Single-resource bodies, consisting of one single file, defined by the two headers: Content-Type and Content-Length.
- Multiple-resource bodies, consisting of a multipart body, each containing a different bit of information. This is typically associated with HTML Forms.

## HTTP Response

![](images/HTTP_Response_Headers2.png)

Bodies can be broadly divided into three categories:

- Single-resource bodies, consisting of a single file of known length, defined by the two headers: Content-Type and Content-Length.
- Single-resource bodies, consisting of a single file of unknown length, encoded by chunks with Transfer-Encoding set to chunked.
- Multiple-resource bodies, consisting of a multipart body, each containing a different section of information. These are relatively rare.

## HTTP Headers

Headers can be grouped according to their contexts:

- **General header:** Headers applying to both requests and responses but with no relation to the data eventually transmitted in the body.
- **Request header:** Headers containing more information about the resource to be fetched or about the client itself.
- **Response header:** Headers with additional information about the response, like its location or about the server itself (name and version etc.).
- **Entity header:** Headers containing more information about the body of the entity, like its content length or its MIME-type.

> ***The list below is not exhaustive, just those that are immediately relevant to this course.***

### Caching
- **Age:** The time in seconds the object has been in a proxy cache.
- **Cache-Control:** Specifies directives for caching mechanisms in both, requests and responses.
- **Expires:** The date/time after which the response is considered stale.

### Conditionals
- **Last-Modified:** It is a validator, the last modification date of the resource, used to compare several versions of the same resource. It is less accurate than ETag, but easier to calculate in some environments. Conditional requests using If-Modified-Since and If-Unmodified-Since use this value to change the behavior of the request.
- **ETag:** It is a validator, a unique string identifying the version of the resource. Conditional requests using If-Match and If-None-Match use this value to change the behavior of the request.

### Connection management
- **Connection:** Controls whether or not the network connection stays open after the current transaction finishes.
- **Keep-Alive:** Controls how long a persistent connection should stay open.

### Content negotiation
- **Accept:** Informs the server about the types of data that can be sent back. It is MIME-type.
- **Accept-Encoding:** Informs the server about the encoding algorithm, usually a compression algorithm, that can be used on the resource sent back.

### Cookies
- **Cookie:** Contains stored HTTP cookies previously sent by the server with the Set-Cookie header.
- **Set-Cookie:** Send cookies from the server to the user agent.

### CORS
- **Access-Control-Allow-Origin:** Indicates whether the response can be shared.

### Downloads
- **Content-Disposition:** Is a response header if the ressource transmitted should be displayed inline (default behavior when the header is not present), or it should be handled like a download and the browser should present a 'Save As' window.

### Message body information
- **Content-Length:** indicates the size of the entity-body, in decimal number of octets, sent to the recipient.
- **Content-Type:** Indicates the media type of the resource.
- **Content-Encoding:** Used to specify the compression algorithm.
- **X-Forwarded-For:** Identifies the originating IP addresses of a client connecting to a web server through an HTTP proxy or a load balancer.

## HTTP Verbs

HTTP defines a set of request methods to indicate the desired action to be performed for a given resource. Although they can also be nouns, these requests methods are sometimes referred as HTTP verbs. Each of them implements a different semantic, but some common features are shared by a group of them: e.g. a request method can be safe, idempotent, or cacheable.

- **GET:** The GET method requests a representation of the specified resource. Requests using GET should only retrieve data.
- **HEAD:** The HEAD method asks for a response identical to that of a GET request, but without the response body.
- **POST:** The POST method is used to submit an entity to the specified resource, often causing a change in state or side effects on the server
- **PUT:** The PUT method replaces all current representations of the target resource with the request payload.
- **DELETE:** The DELETE method deletes the specified resource.
- **CONNECT:** The CONNECT method establishes a tunnel to the server identified by the target resource.
- **OPTIONS:** The OPTIONS method is used to describe the communication options for the target resource.
- **TRACE:** The TRACE method performs a message loop-back test along the path to the target resource.
- **PATCH:** The PATCH method is used to apply partial modifications to a resource.

## HTTP Status Codes

- **100:** Information responses.
- **200:** Successful responses.
    - *200:* Ok.
    - *204:* No Content.
- **300:** Redirection messages.
    - *304:* Not Modified.
    - *308:* Permanent redirect.
- **400:** Client error responses.
    - *400:* Bad Request.
    - *403:* Forbidden.
    - *404:* Not Found.
- **500:** Server error responses.
    - *500:* Internal Server Error
    - *503:* Service Unavailable

# References

- [MDN HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)