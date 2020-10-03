---
title: "SEM5640 Lecture 2 - JakartaEE"
date: 2020-09-28T14:00:00+0000
categories: [Lecture Notes]
tags: [SEM5640,JavaEE]
---
## JakartaEE

* Java = Language/Platform
* Platform = JVM+API
* 4 Platforms
  * JavaSE
  * JavaEE
  * JavaME
  * JavaFX

* Provides
  * Development model
  * APIs
  * Runtime Environment
* For developing and running multi-tiered, scalable, reliable and secure network systems.
  * i.e.  Enterprise Applications
![Tier Diagram](/assets/img/tier-diagram.png "Tier Diagram")

## Web Tier

* Access via HTTP
* Dynamic pages generally
* Handle client requests
* Screen Flow
* JavaBeans for temp storage
* Simple logic
  * Reasons not use it
    * Lightweight
    * better decoupling and distribution of function
    * Not Maximum support

## Business Tier

* Access to Java Objects
* Business Logic
* Application specific
* Available for presentation

## EIS Tier

* On other machines
* "Foreign" tech
* Can be legacy tech
* Often separately managed
* Can be separately accessed

![Tier Diagram](/assets/img/tier-diagram-with-links.png "Tier Diagram with client links")

## Clients

* Web Client(thin)
  * Makes HTTP Requests
  * Dynamic results
  * JS/AJAX
  * Browser
* Application Client
  * Java/other lang
    * GUI
    * CLI
  * Direct access to business tier
* Application client in another server
  * Can have no UI

## Distribution

* Web tier and Business tier on different servers
* Business tier accessed by different web tiers
* Either or both replicated
  * horizontal scaling
  * load balancing mechanisms required

## Jakarta EE Application Servers

* Open Source
  * JOnAS
  * WildFly (was JBoss, now under RedHat)
  * Geronimo - Apache
  * Glassfish- reference implementation
  * Payara - fork of Glassfish
  * Tomcat (Apache, web profile), TomEE
  * Jetty - limited, embeddable, testing
* Commercial Servers
  * WebLogic (Oracle)
  * WebSphere (IBM)
  * JBoss (Red Hat)

* Additional Services
  * e-mail client
  * messaging
  * database connections
  * messaging...
  * configurable
  * to support applications loaded onto the server
  * guaranteed by the spec.

## Java EE Components - the applications

* Self Contained
  * Communicate with other units
  * may use standard classes
* JavaEE
  * Application clients/Applets
  * Web components
    * Java Servlets
    * JavaServer Pages (JSP) (based on servlets)
    * JavaServer Faces (JSF) (based on servlets)
  * Business Components
    * Enterprise Java Beans (EJB)
* Business Tier
  * JAX-RS - RESTful web services
  * JAX-WS web services endpoints
  * Java Persistance API entities

## Java EE Application Server

Provides

* JVM/Core API
* EE API
* component containers
  * component lifecycle management
    * creation
    * association with called code
    * life span
  * services to components
    * security
    * transaction management
    * directory lookups
    * remote connectivity
* Runs continuously

## Containers

* On a Client
  * Application Client Container
  * (Applet Container)
* Java EE Application Server
  * Web Container
  * Web pages, servlets, some EJB components
* Enterprise JavaBeans (EJB) container
  * EJBs

## Deployment

* Components
  * Java Classes
  * how
    * what url
    * Who can access
    * What can they access
  * Included in JAR
  * Deployed in two methods
    * Deployment descriptors
    * Annotations

## Deployment Descriptors

* XML
* Config
* Components
* change details
  * Without code
  * Different deployments
  * Override defaults
* general (web.xml) or specific (sun-web.xml)

## Annotations

* @Keyword
* Annotates java code
  * Can change how code is handled
    * Tells it is a web component
* Annotation in JavaEE
  * Widely used
  * Deployment information
  * Newer mechanism
  * Overridden by deployment descriptors if present

* Deployment formats
  * Jar format
  * Components plus deployment descriptors - a module
  * Each for one container type
  * Internal structure defined
  * EE Modules
    * Web modules .war
    * EJB modules .jar
    * Application client modules .jar
    * Resource Adapter Modules .rar
  * Enterprise Archive
  * A set of modules .ear

![War Structure](/assets/img/war-structure.png ".war Structure")
JavaEE
## JavaEE versions

* J2EE 1.2 (1999)
* ...
* Java EE 5 (2006)
* ...
* Java EE 7 (2013)
* Java EE 8 (Aug 31, 2017)
* Jakarta EE 8 (Sept 2019)
* Jakarta EE 9 (Target: August 31, 2020)

## links

* [Jakarta Website](https://jakarta.ee/)
* [Your First Cup: An Introduction to the Java EE Platform](https://javaee.github.io/firstcup/)
* [Example github for first cup](https://github.com/eclipse-ee4j/jakartaee-firstcup-examples)
* [The Jakarta EE 8 Tutorial](https://eclipse-ee4j.github.io/jakartaee-tutorial/)
* [API](https://javaee.github.io/javaee-spec/javadocs/)

## Jakarta EE Development and deployment

* An application server is required
  * Provides the containersIs a web server
  * has the JVM
  * has the libraries (available for load) to provide the APIs

* code on a server can be used to run≥1 “domain”
  * defined by a directory structure
  * can be start/stopped
  * can be deployed to
  * potentially>1 “application”
  * has logs etc.
  * requires management

## Glassfish management

* CLI -asadmin(see deployment guide
  * huge set of complex options
  * necessary complexity
  * excellent for automation - scripts
* Web interface
  * an available “application”
  * on https port 4848 by default
  * (other applications on http 8080, https 8181 by default)
  * “manual” therefore
* Deployment
  * either of the above (therefore potentially remote)
  * copy a jar into a specific directory in the domain structure
    * "autodeploy”

## Tools we will use

* Java EE 8 / Jakarta EE 8
* therefore Java 1.8
* NetBeans 8
* Maven (https://maven.apache.org/)
* Glassfish 4

* Own machines
  * Netbeans 11
  * Payara 5
  * Java 1.8
