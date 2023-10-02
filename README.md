# HTTP Testing

[![license](https://img.shields.io/github/license/interlok-testing/testing_http.svg)](https://github.com/interlok-testing/testing_http/blob/develop/LICENSE)
[![Actions Status](https://github.com/interlok-testing/testing_http/actions/workflows/gradle-build.yml/badge.svg)](https://github.com/interlok-testing/testing_http/actions/workflows/gradle-build.yml)

Project tests interlok-apache-http, interlok-okhttp, interlok-json features

## What it does

This project has a single workflow that implements a simple rest api with a jetty consumer and that make three http requests to an api using standard http service, apache http service and ok http service. The result of the three responses is aggregated to a json response.

![HTTP Diagram](/http-diagram.png "HTTP Diagram")

## Getting started

* `./gradlew clean build`
* `(cd ./build/distribution && java -jar lib/interlok-boot.jar)`

The config is using a variables.properties to configure the api path, the request api url and mthod and the json path to extract response data.

```
apiPath=/api/chuck-norris-jokes
requestApiHost=https://api.chucknorris.io
requestApiUrl=${requestApiHost}/jokes/random
httpMethod=GET
extractXpath=$.value
```

## Try it

You can call the api with the following curl command:

`curl --location --request GET 'http://localhost:8080/api/chuck-norris-jokes'`

You should receive something like:

```
{
  "jokeApache" : "The only child ever to survive a roundhouse kick by Chuck Norris was Gary Coleman. He has not grown since.",
  "jokeOk" : "Chuck Norris changes saw blades while using the saw!",
  "jokeStandard" : "Chuck Norris' shit easily sinks lower than whale shit."
}
```

## Test it

All the services used in this config are tested via the service tester.
The external http call are mocked using interlok-service-tester-wiremock.

To run the tests you can either use the UI Service Test page or run:

`./gradlew clean check`

