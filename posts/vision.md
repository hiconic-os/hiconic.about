# Hiconic Vision

_Let's give modeling a chance._

## Overview

The purpose of this document about _Hiconic_ is to show:
* some of the key ideas behind it on a high level
* how it differs from other frameworks
* it's power that leads to simplicity


_NOTE: For the sake of brevity we only show a small subset of the platform's perks._

<!--
Lastly, we discuss the broader advantages of our approach, including in the context of artificial intelligence.
-->

## Context

### State of SW Development

Let's set the stage by a few (bold) claims about various aspects of current SW development:
* **modeling support** - data types are treated as second class citizens by programming languages
* **model advantages** - data types are underappreciated and underutilized
* **convention over configuration** - modern frameworks aren't convenient enough
* **agility** - developers are being bothered by technical details
* **portability** - code is not portable enough


### Problem outline

To illustrate these points, let's consider the following question: \
**What is the simplest way to create a backend application?**

Such an app is quite basic - it defines a set of requests a client can make (API), and for each request sends back a response.

The developer thus has to do 3 things:
* define the API (requests)
* implement the services
* offer a way for the client to make a request

## The _Hiconic_ Way

Let's see how simple implementing a backend application is with _Hiconic_.

We'll go with a single request - `Greet` - with a parameter called `name`, which responds `Hello` to the person with given name (e.g. `Hello John`).

_NOTE: We show a simplified, less technically correct example, compared to a real implementation ([see tutorial](https://hiconic-os.github.io/hiconic.platform.reflex/getting-started/getting-started.html)). It is to avoid technical details, irrelevant at this level, in favor of paradigm clarity._

### Defining the API

Our way to define an API is to model the requests, i.e. create an entity type for each request.

```java
entity Greet extends ServiceRequest {
    String name

    String eval()
}
```

### Implementing the service

This is a straight forward (_Java_) code, packaged as a module:

```java
public class GreetProcessor implements ServiceProcessor<Greet> {
    public String process(Greet request) {
        return "Hello " + request.name;
    }
}
```

_NOTE: We also need to binds this processor to the `Greet` request, which is straight forward but let's ignore that syntax for now._

### Offering an endpoint to the client

Let's say we want to deploy our service as a web application accessible over _REST_.

In our world, an application is just a shell, which defines the platform (e.g. _Reflex_, our microservices platform) and a list of modules. So we do just that:
* hiconic-reflex-platform
* greet-module (which brings our model as its dependency)
* web-server-module
* rest-endpoint-module

**Aaaand that's it, so easy!**

We can now build the app, deploy it, access via `example.com/api/greet?name=World` and get `"Hello World"` back.

## Dissecting the _Hiconic_ Way

Let's see what we did (or didn't have to do), and how have we addressed the [aspects](#state-of-sw-development) we mentioned at the beginning:

We have **modeled** our API so to call a service a request instance needs to be created and evaluated. This has many **advantages**, e.g.:
* request instance is easy to intercept and modify based on its type hierarchy or metadata configuration
* ideal for microservices, forces communication over APIs
* ideal for clients, natural fit for asynchronous programming
* in code, evaluating a request instance hides the underlying protocol; you might not even know if you're evaluating it locally or talking to a remote server

We have NOT, however, bothered the backend developer with mapping the request to the URL. The mapping is automatic, based on request name and its properties - **convention over configuration**.

As for **agility**, we also didn't define the response's format (e.g. JSON). For us, what matters is the modeled return type (i.e. structure of the data), not the way it's serialized. It is up to client to describe what format they want, JSON is just default.

_NOTE: Yes, our service returned just text, but it is JSON - see the quotes around the text._

**Portability** is achieved by packaging our service as a module, independent of where it will be deployed and how it will be accessed. We went with a REST based web application, but it could be:
* RPC based web application
* event listener (Apache Kafka)
* command line application
* anything else (e.g. smartphone application with generic UI)

Our platform is built for **modeling** with lots of tools and features. We treat models as an extension of the language, entities as separate types (besides classes and interfaces) with their own reflection. This makes any kind of domain-independent task easy to implement with elegant and efficient code (e.g. serializing as JSON or auto-mapping URL parameters).

## Further reading

* [State of the Art](state-of-the-art.md) - explains where we are; what's already done, what's work in progress and what's on the roadmap