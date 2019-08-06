## What is Swagger?
Swagger is a specification and complete framework implementation for describing, producing, consuming, and visualizing RESTful web services. The overarching goal of Swagger is to enable client and documentation systems to update at the same pace as the server. The documentation of methods, parameters and models can be tightly integrated into the server code, allowing APIs to always stay in sync.

## What is _The OpenAPI Specification_?

The Open API Initiative (OAI) was created by a consortium of forward-looking industry experts who recognize the immense value of standardizing on how REST APIs are described. As an open governance structure under the Linux Foundation, the OAI is focused on creating, evolving and promoting a vendor neutral description format. SmartBear Software is donating the Swagger Specification directly to the OAI as the basis of this Open Specification. 
APIs form the connecting glue between modern applications. Nearly every application uses APIs to connect with corporate data sources, third party data services or other applications. Creating an open description format for API services that is vendor neutral, portable and open is critical to accelerating the vision of a truly connected world.

> ### tl;dr
> Swagger was originally developed as a part of Wordnik, and was bought by SmartBear, the company behind other service-oriented products such as SOAPUI. They open sourced most of the Swagger source code, but kept it under their stewardship. In an attempt to create an open ecosystem they seperately created the OpenAPI Initiative to steward the specification _itself_.

## Why is Swagger Useful?

The Swagger framework simultaneously addresses server, client, and documentation/sandbox needs for REST APIs. As a specification, it is language-agnostic. It also provides a long runway into new technologies and protocols beyond HTTP.

With Swagger's declarative resource specification, clients can understand and consume services without knowledge of server implementation or access to the server code. The Swagger UI framework allows both developers and non-developers to interact with the API in a sandbox UI that gives clear insight into how the API responds to parameters and options. Swagger happily speaks both JSON and XML, with additional formats in the works.

## Quick Introduction

Swagger is made up of three components:

- Server: hosts the REST APIs description that you want to use.
- Client: uses the REST APIs description from the server.
- UI: Reads a description of the APIs from the server and renders it as a web-page and an interactive sandbox to play with the APIs.

### Server

The typical place to start with a Swagger implementation is with the server. A server will have some number of APIs as well as a api-docs url (something like `http://yourhost.com/api-docs`). The api-docs URL is the starting point for Swagger. It contains a JSON description of the resources that are available.

### Client

The client is any application that wants to use the APIs on the server. The client is given a URL that points to the api-docs and converts the JSON into an object that can used to call the REST APIs. Clients are available in any number of languages, making it very easy to quickly implement REST APIs that have been documented with Swagger without requiring much new code.

### UI

Finally, the Swagger UI serves a double-purpose as documentation and a way to enable developers to play around with the REST APIs without actually having to write any code. The default Swagger UI can be seen at the pet store demo. The default Swagger UI includes a box at the top of the screen for typing in the URL for any api-docs. Since the Swagger UI is completely dynamic, it will read in the api-docs from any site and render the API documentation and enable the calling of the REST APIs. The default Swagger UI can be installed through npm install swagger-ui, and the HTML templates can be modified to your liking.

### Creating Your Swagger Specification

The api-docs URL that typically lives on the server and is used by both the client and the Swagger UI is referred to as a Swagger Specification. The Swagger Specification is made up of two files:

- Resource Listing: Lists the APIs that are available and gives a brief description of them.
- API Description: Detailed description of each API in the Resource Listing, including both the functional description (parameters, function names, return values) and human-readable description of how to use the API.
- The actual api-docs URL is a Resource Listing JSON that describes the Swagger resources that are available, where they live, and how to use them. If you type the api-docs URL into your browser, you will see the resource listing.

There are three ways to create a Swagger Specification, depending on which server you are using:

- Codegen: This is the traditional way of creating a Swagger Specification. The swagger codegen converts annotations in your code into the Swagger Specification.
- Automatically: Some servers, such as swagger-node-express and swagger-play, will create both your REST APIs and your Swagger Specification for you at the same time.
- Manually: And finally, you can always create your Swagger specification by writing the JSON by hand. After you write your Swagger specification (or if you get a Swagger specification from a different server) you can use one of the Server generators to create your code, such as the node.js server generator


# References

- [OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification)
- [Swagger](http://swagger.io/)