RESTful (REpresentational State Transfer) services are an architectural style for building services that closely model and leverage off of HTTP. To achieve this we enforce a set of self-imposed, high-level constraints that limits how we design our end points. While there is no absolute set of rules, these guiding principles result in predictable, explorable and lean API - so much so that RESTful services have become the _de facto_ standard of the Web.

> The foundations of REST as an architectural style were set be Roy Fielding in his PhD Dissertation on _Architectural Styles and the Design of Network-based Software Architectures_. This was based on his experience as a contributor to the HTTP specification.


> _"Throughout the HTTP standardization process, I was called on to defend the design choices of the Web. That is an extremely difficult thing to do within a process that accepts proposals from anyone on a topic that was rapidly becoming the center of an entire industry. I had comments from well over 500 developers, many of whom were distinguished engineers with decades of experience, and I had to explain everything from the most abstract notions of Web interaction to the finest details of HTTP syntax. That process honed my model down to a core set of principles, properties, and constraints that are now called REST."_ - Roy Fielding, 11 Nov 2009.


## Architectural Properties
The desirable architectural properties of a RESTful api are:

- **Performance**
- **Scalability** 
- **Simplicity**
- **Modifiability** (even while the application is running)
- **Visibility** (transparency)
- **Portability**
- **Reliability**

## Architectural Constraints

### Client-Server

The first constraint of a RESTful application style is that a distinct client-server model is enforced - as a clear separation of concerns. The client must not have any understanding of the data storage - for example. Significantly, this separation allows the front end and services to evolve independently.

### Stateless
Communication between the client and server must be stateless - each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server - and allows for much greater visibility, reliability, and scalability, at the potential cost of some performance.

### Cache

To partially mitigate the cost of the stateless constraint, the RESTful architectural style prescribes that all data within a response to a request must be implicitly or explicitly labeled as cacheable or non-cacheable. 

### Uniform interface:  

The uniform interface constraint defines the interface between clients and servers. It simplifies and decouples the architecture, which enables each part to evolve independently. The four guiding principles of the uniform interface are:

#### Resource-Based
Individual resources are identified in requests using URIs as resource identifiers. The resources themselves are conceptually separate from the representations that are returned to the client.

#### Manipulation of Resources Through Representations
When a client holds a representation of a resource, including any metadata attached, it has enough information to modify or delete the resource on the server, provided it has permission to do so.

#### Self-descriptive Messages
Each message includes enough information to describe how to process the message.

#### Hypermedia as the Engine of Application State (HATEOAS)
Clients deliver state via body contents, query-string parameters, request headers and the requested URI (the resource name). Services deliver state to clients via body content, response codes, and response headers


## Layered system

A client cannot ordinarily tell whether it is connected directly to the end server, or to an intermediary along the way. Intermediary servers may improve system scalability by enabling load-balancing and by providing shared caches.


## Code on demand (optional)

Servers are able to temporarily extend or customize the functionality of a client by transferring logic to it that it can execute. Examples of this may include compiled components such as Java applets and client-side scripts such as JavaScript.


> Complying with these constraints, and thus conforming to the REST architectural style, will enable any kind of distributed hypermedia system to have desirable emergent properties, such as performance, scalability, simplicity, modifiability, visibility, portability and reliability.

## Relationship to HTTP

HTTP is more than just a transport over which REST services are exposed. A RESTful architecture will embrace and leverage off of the design of HTTP, most particularly the HTTP Headers and HTTP Verbs.

## HTTP Headers
As a REST service is supposed to be self contained and stateless, but is only supposed to consume and produce representations of state, we leverage off the HTTP Headers to contain everything else. HTTP Headers are suitable for containing service meta-information (such as encoding and content type), as well as authentication and session information (such as identity tokens, authorization keys).

## HTTP Verbs
RESTful services typically make use of a much wider range of HTTP Verbs, using them to act on resources and carry semantic meaning. The closer you are to embracing the pure semantic nature of the verbs, the more explorable your API will be. Someone reading the api will immediately associate a request that uses a PUT, GET or DELETE verb with it being idempotent.

## Resources
In addition to utilizing the HTTP verbs appropriately, resource naming is arguably the most debated and most important concept to grasp when creating an understandable, easily leveraged Web service API. When resources are named well, an API is intuitive and easy to use. Done poorly, that same API can feel klutzy and be difficult to use and understand. Below are a few tips to get you going when creating the resource URIs for your new API.

Essentially, a RESTful API ends up being simply a collection of URIs, HTTP calls to those URIs and some JSON and/or XML representations of resources, many of which will contain relational links. The RESTful principal of addressability is covered by the URIs. Each resource has its own address or URI—every interesting piece of information the server can provide is exposed as a resource. The constraint of uniform interface is partially addressed by the combination of URIs and HTTP verbs, and using them in line with the standards and conventions.

In deciding what resources are within your system, name them as nouns as opposed to verbs or actions. In other words, a RESTful URI should refer to a resource that is a thing instead of referring to an action. Nouns have properties as verbs do not, just another distinguishing factor.

Some example resources are:

- Users of the system.
- Courses in which a student is enrolled.
- A user's timeline of posts.
- The users that follow another user.
- An article about horseback riding.

Each resource in a service suite will have at least one URI identifying it. And it's best when that URI makes sense and adequately describes the resource. RESTful APIs are written for consumers, and the name and structure of URIs should convey meaning to those consumers.

<table class="table table-striped table-bordered">
    <thead>
        <tr>
            <th>HTTP Verb</th>
            <th>CRUD</th>
            <th>Entire Collection (e.g. /customers)</th>
            <th>Specific Item (e.g. /customers/{id})</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>POST</td>
            <td>Create</td>
            <td>201 (Created), 'Location' header with link to /customers/{id} containing new ID.</td>
            <td>404 (Not Found), 409 (Conflict) if resource already exists..</td>
        </tr>
        <tr>
            <td>GET</td>
            <td>Read</td>
            <td>200 (OK), list of customers. Use pagination, sorting and filtering to navigate big lists.</td>
            <td>200 (OK), single customer. 404 (Not Found), if ID not found or invalid.</td>
        </tr>
        <tr>
            <td>PUT</td>
            <td>Update/Replace</td>
            <td>404 (Not Found), unless you want to update/replace every resource in the entire collection.</td>
            <td>200 (OK) or 204 (No Content).  404 (Not Found), if ID not found or invalid.</td>
        </tr>
        <tr>
            <td>PATCH</td>
            <td>Update/Modify</td>
            <td>404 (Not Found), unless you want to modify the collection itself.</td>
            <td>200 (OK) or 204 (No Content).  404 (Not Found), if ID not found or invalid.</td>
        </tr>
        <tr>
            <td>DELETE</td>
            <td>Delete</td>
            <td>404 (Not Found), unless you want to delete the whole collection—not often desirable.</td>
            <td>200 (OK).  404 (Not Found), if ID not found or invalid.</td>
        </tr>
    </tbody>
</table>

## What makes REST design difficult?
RESTful APIs are difficult to design because REST is an architectural style, and not a specification. It has no standard governing body and therefore has no hard and fast design rules. What REST does have is an interpretation of how HTTP protocol works, which allows for lots of different approaches for designing a REST API. While use of HTTP methods is a core advantage of the REST approach, it also means that there are lots of different RESTful API designs.

## Versioning

This is a very important aspect that is often overlooked. As an API provider, one of your most important tasks is to make sure that breaking changes will never occur in your API. Making breaking changes will make life difficult for the developers who depend on your service and can easily start causing frustration when things start to break.

There are two primary approaches to versioning RESTful services, using an HTTP Header or using the URL. While there are many examples of using an HTTP Header in the wild, the most common is to version the URL - as this gives you the greatest flexibility and addresses the 'Layered System' constraint. 

For example:

```http
GET /v1/geocode HTTP/1.1
Host: api.geocod.io

GET /v2/geocode HTTP/1.1
Host: api.geocod.io
```

## URL structure
The URL structure is one of the most important pieces of the puzzle. Spending some time to define the right endpoint names can make your API much easier to understand and also help making the API more predictable.

URLs should be short and descriptive and utilize the natural hierarchy of the path structure. It’s also important to be consistent with pluralization.

If you are working with objects, keep the object id in the URL and leave everything else to the query string.

Let’s take a store locator API as an example. Here are some possible endpoints:

- `/v1/stores/1234` – Return the store that has id 1234
- `/v1/stores/1234/report` – Report an error for the store with id 1234
- `/v1/stores` – Return all stores
- `/v1/stores/near?lat=12.34&lon=-12.34` – Find stores near a given location
- `/v1/categories` – Return a list of store categories

Combining these URLs with the semantically appropriate HTTP Verbs creates a very rich API. Consider the following with just `/v1/stores/1234`:

|HTTP Verb|	Description|Example|
|---|---|---|
|GET|	This is the most common verb, and is used to retrieve data | GET /v1/stores/1234|
|PUT|	PUT requests are commonly used to update/replace an object | PUT /v1/stores/1234|
|POST|	This is used to create a new instance of an object | POST /v1/stores|
|DELETE|	As the name suggests, this will delete the object | DELETE /v1/stores/1234|

# References:

- [Roy Fielding Dissertation](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)
- [REST vs SOAP](https://stormpath.com/blog/rest-vs-soap)
- [REST API Tutorial](https://github.com/tfredrich/RestApiTutorial.com)
- [Nouns are Good, Verbs are Bad](https://apigee.com/about/blog/technology/restful-api-design-nouns-are-good-verbs-are-bad)
- [Plural Nouns and Concrete Names](https://apigee.com/about/blog/technology/restful-api-design-plural-nouns-and-concrete-names)
- [Designing a Restful Web API](https://scotch.io/bar-talk/designing-a-restful-web-api)