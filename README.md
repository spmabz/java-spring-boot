# https://github.com/geryb-bg/java-spring-boot

# Swagger + SpringFox + SpringBoot example

This is a simple example to demonstrate Swagger with Spring Boot.  The integration
is handled by SpringFox, a 3rd party library for enabling Swagger on Spring MVC projects.

For more information on SpringFox, pleas visit [http://springfox.io](http://springfox.io)

This demo is from [this repo](https://github.com/swagger-api/swagger-samples/tree/master/java/java-spring-boot)

To run this do the following:

- `mvn clean package`
- `java -jar target/swaggerhub-spring-boot-sample-1.0.0-SNAPSHOT.jar`


- To check if it's working: http://localhost:8080/v2/pets/1
- To get to swagger UI: http://localhost:8080/v2/swagger.json
- To get to swagger UI: http://localhost:8080/v2/index.html

## LAB

Your task is to build a RESTful Pet Store API, which must fulfill the requirements listed below. The three resources that need to be modeled are the pets, the store, and the users.

Use your best judgment.

The api must be able to:

- add a new pet to the Store.
- update an existing pet, both with complete and with - partial data.
- find a pet by id.
- find pets by a status.
- upload an image for the pet.
- return an aggregated list of the number of pets per - status.
- place an order for a pet.
- cancel an order for a pet.
- find an order by its id.
- create a user
- find a user by user name
- delete a user
- update a user
- let a user log in
- let a user log out

# References

## HTTP

- [MDN HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)

## RPC

- [Wikipedia: Remote Procedure Call](https://en.wikipedia.org/wiki/Remote_procedure_call)
- [Wikipedia: Idempotence](https://en.wikipedia.org/wiki/Idempotence)
- [Wikipedia: XML-RPC](https://en.wikipedia.org/wiki/XML-RPC)

## JSON

- [JSON](http://www.json.org/)
- [JSON Schema](http://json-schema.org/)
- [Understanding JSON Schema](https://spacetelescope.github.io/understanding-json-schema/)

## REST

- [Roy Fielding Dissertation](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)
- [REST vs SOAP](https://stormpath.com/blog/rest-vs-soap)
- [REST API Tutorial](https://github.com/tfredrich/RestApiTutorial.com)
- [Nouns are Good, Verbs are Bad](https://apigee.com/about/blog/technology/restful-api-design-nouns-are-good-verbs-are-bad)
- [Plural Nouns and Concrete Names](https://apigee.com/about/blog/technology/restful-api-design-plural-nouns-and-concrete-names)
- [Designing a Restful Web API](https://scotch.io/bar-talk/designing-a-restful-web-api)

## The Richardson Maturity Model

- [Richardson Maturity Model](https://martinfowler.com/articles/richardsonMaturityModel.html)
- [Rest APIs must be hypertext-driven, 2010](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven)
- [Rest Cook Book](http://restcookbook.com)

## OpenAPI

- [OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification)
- [Swagger](http://swagger.io/)