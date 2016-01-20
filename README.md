# OpenDSB - core

OpenDSB is a distributed Open-Source Service Bus. 

## Introdution

> In today's world, real-time information is continuously getting generated by applications (business, social, or any other type), and this information needs easy ways to be reliably and quickly routed to multiple types of receivers. Most of the time, applications that are producing information and applications that are consuming this information are well apart and inaccessible to each other. This, at times, leads to redevelopment of information producers or consumers to provide an integration point between them. Therefore, a mechanism is required for seamless integration of information of producers and consumers to avoid any kind of rewriting of an application at either end. (Nishant Garg)

As developers, we work in a world of abstractions. Each piece of technology 
that we use is built upon layers and layers of other systems. This allows 
us to build software more efficiently. Frameworks such as Ruby on Rails, 
Django, Play Framework, Spring Roo and Express were created to abstract 
away the painful parts of web development. They set up standards and 
best practices to build web applications. We have all of these amazing 
tools to build applications. 
Nowadays, in this world of Docker containers, to implement applications using 
the micro-services architecture we need a bus events, but that is supported 
in a distributed environment, where each component can be running in a 
container. Existing solutions are very heavy and do not meet current 
requirements. The idea here is to develop a lightweight solution that can 
be used in Java, JavaScript and Golang and can integrate assorted environments.

## Description

OpenDSB is an open source, distributed publish-subscribe messaging system, 
mainly designed with the following characteristics:

* High throughput: Keeping big data in mind, OpenDSB is designed to work on commodity hardware and to support millions of messages per second.
* Distributed: OpenDSB explicitly supports messages partitioning over OpenDSB servers and distributing consumption over a cluster of consumer machines while maintaining per-partition ordering semantics.
* Multiple client support: OpenDSB system supports easy integration of clients from different platforms such as Java, JavaScript and Golang.
* Real time: Messages produced by the producer threads should be immediately visible to consumer threads; this feature is critical to event-based systems such as [Complex Event Processing (CEP)](https://en.wikipedia.org/wiki/Complex_event_processing) systems.

In the present big data era, the very first challenge is to collect the data 
as it is a huge amount of data and the second challenge is to analyze it.

Message publishing is a mechanism for connecting various applications with 
the help of messages that are routed between them, for example, by a 
message broker such as OpenDSB broker. OpenDSB broker is a solution to 
the real-time problems of any software solution, that is, to deal with 
real-time information and route it to multiple consumers quickly. 
OpenDSB provides seamless integration between information of producers 
and consumers without blocking the producers of the information, 
and without letting producers know who the final consumers are.

## Architeture

TBD

## Using OpenDSB

### Docker Image

We have an image that includes Java **OpenJDK 9**, build 96 
(available in https://jdk9.java.net/download/) with **REPL** 
support via **jshell**

This image allows you to work in the Service Bus as if it were in a playground.
It provides plenty productivity in the typical development workflow.

#### Building the image

    mkdir opendsb && cd opendsb
    git clone git@github.com:opendsb/core.git
    cd core
    ./build-opendsb

#### Protecting passwords and credentials 

    touch .credentials
    # edit file with your preferred editor. This file is listed in .gitignore

#### Running the container 

    docker run -i -t --rm --name dsb parana/opendsb

Now you can invoke `jshell` and run some commands:

    /imports
    /methods
    /help

and so on.

To quit use the `/exit` jshell command.

### Running opendsb using Heroku to provide Continuos Delivery

We will use [Spark Template Engine](https://github.com/perwendel/spark) in our examples. 

This Workflow is very productive.

https://github.com/heroku/heroku-cli is client written in Golang

    heroku login

#### Running Locally

Make sure you have Java and Maven installed.
Also, install the [Heroku Toolbelt](https://toolbelt.heroku.com/).

```sh
mvn install
java -cp target/classes:target/dependency/* Main
http://localhost:9095/
# You can use foreman, but this run only on Linux
# foreman start web 
```

Your app should now be running on [localhost:9095](http://localhost:9095/).

If you're going to use a database, ensure you have a local `.env` 
file that reads something like this:

```
DATABASE_URL=postgres://localhost:5432/java_database_name
```

#### Deploying to Heroku

```sh
heroku create opendsb --buildpack heroku/java
git add .
git commit -m "Heroku Support"
# pom.xml must appear on git list files command
git ls-files | grep pom.xml
git push heroku master
# this command open https://opendsb.herokuapp.com in your Safari browser
heroku open
```

#### Documentation

For more information about using Java on Heroku, see these Dev Center articles:

- [Java on Heroku](https://devcenter.heroku.com/categories/java)
