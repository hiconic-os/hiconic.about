# State of the Art

Where we are and where we're going:

## Core Technology

* Our codebase is primarily _Java_.
* Core of our tech are the models, with multiple tools and platforms built on top.
* We don't support a dedicated syntax for entities yet. We declare entities as _Java_ interfaces, with classes being implemented automatically.
* Writing generic code for our entities is easy and the code is fast. Serializing to JSON takes ~25% less time than industry standard `jackson-databind`, for example.
* Our entities are more flexible than other frameworks. We support multiple inheritance and cyclic references.
* Currently we only support development with `Eclipse` with our plugins, and a custom build tool implemented on top of `Gradle` (and `Ant` which we'll get rid of).

## Platforms

* **Cortex** is a modular monolith platform that's been developed for years and there are a few commercial instances running live. It is powerful, yet bulky.
* **Reflex**, a modular microservices platform, is a recent initiative. A very lightweight core was written from scratch and lots of features can be directly migrated from _Cortex_. It already supports REST and RPC web endpoints, but can also be packaged as a command line tool.
* Our models are also supported in _JavaScript_/_TypeScript_ for frontend development. We can also envision a pure _Node.js_ implementation. Our modeled requests are a natural fit for asynchronous programming.
* We have a so-called **"step-framework"**, built for _Gradle_, which makes big chunks of our pipeline scripts portable.

## Work in Progress

* Support popular tools like _Gradle_ and IDEs like _IntelliJ IDEA_.
* Migrate more **Cortex** modules to **Reflex** to make it real world ready.
* Explain to people how consequent application of modeling leads to repeated patterns beneficial for both human and artificial intelligence.

## Roadmap

* Codebase cleanup to make it easier for outsiders.
* Release in _Maven Central_.
* Pre-compile entities, rather than generate bytecode at runtime to improve startup time.
* Support native images on _GraalVM_..
* Improve _JavaScript_ support, offer a more lightweight library that loads quickly.
* Support dedicated syntax for entities.
