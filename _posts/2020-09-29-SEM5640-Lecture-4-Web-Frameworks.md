---
title: "SEM5640 Lecture 4 - Web Frameworks"
date: 2020-09-29T10:00:00+0000
categories: [Lecture Notes]
tags: [SEM5640]
---
## Web application frameworks

* static web pages
  * Ok for some material
  * Most is dynamic
* Dynamic pages
  * Execute code
  * Access the HTTP environment
    * requests and response
  * Access resources
  * Produce HTML (or other)

* The JavaEE Web Container supports servlets by
  * managing their life cycle
  * giving access to HTTP

* Server side coding is:
  * very detailed
  * very repetitive
  * (hard to debug)

## The support we need

* Templating
  * Hard coded print statements are
    * Laborious
    * Error prone
    * Hard to reuse
* Validation
  * HTTP is string
  * Need to validate other units
* Automated Internationalization and Localization
* Call, session and environment management and associated data
  * integrated with templating
* Support for good patterns
* Good patterns exist i.e. MVC
  * Push based
    * actions pushed to view after processing
  * Pull based
    * view components pull from controllers
* Security
  * Sessions
  * Authentication
  * Authorization  
* URL Mapping and navigation
  * hard coded
    * Hard
    * Error Prone
    * Conditional addressing is difficult

* Frameworks
  * ColdFusion
  * Scala
  * Perl
  * PHP: Drupal, CakePHP
  * Python
  * Ruby: Ruby on Rails
  * Java
    * Struts
    * Spring
    * Java Server Faces (JSF)

## JSF under JavaEE

* Templating
  * Facelets
  * (JSP)
* Validators
  * Built in
  * User supplied (Beans)
* MVC Pull
* Navigation
  * Fixed
  * Dynamic
* AJAX

## JavaEE
* Seen i18n and L10n?
* Session Management
  * Seen
  * Integrates with JSF templating
* Security
* Testing Framework
  * JUnit
  * Specialist - container based
* Code reuse
  * Many libraries to use
  * General good reuse in Java

## History and Status Java Server Faces

* 2004 onwards
* Initially part of standard JavaEE
* v1.2 added to JavaEE 2006
* V2.0 released 2009 (JavaEE )Major changes
* V2.1 (maintenance release)
* V2.2 (2013-04-16)V2.3 (2017-03-28)
* Standard JavaEE Web Application Framework
* JSP incorporated, but deprecated
* Others available

## Basic technology

* An API for
  * representing components and managing their state
  * handling events, server-side validation, and data conversion;
  * defining page navigation
  * supporting internationalization and accessibility
  * and providing extensibility
* Tag libraries for
  * adding components to web pages
  * connecting components to server-side objects

## Developer jobs

* Design a web page description
  * Components are tags
* Bind components to server-side data
* Attach events from components to server-side code
* Associate data with a scope
  * persist as required
* Design navigation

## A JSF Application

* web page description with components
* set of tags to add components to the web page
* set of managed beans
* web deployment descriptor (web.xml) and/or annotations
* configuration resource files (or annotations + conventions)
  * faces-config.xml
  * define page navigation rules
  * configure beans and custom components
* set of custom objects
  * components – re-usable composite page elements
  * validators – input validation (if special)
  * converters – convert input strings (if special)
  * listeners – responses to component events
* custom tags for custom components

```xhtml
<? xml   version = ’1.0’ encoding=’UTF−8’?>
<!DOCTYPE html PUBLIC "−//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1−transitional.dtd">
<html xmlns= "http://www.w3.org/1999/xhtml"
    xmlns: h= "http://java.sun.com/jsf/html">
<h :head>
    <title> Faces Title </title>
</h:head>
<h:body>
    <h:graphicImage value="#{resource [’images:logo.png’]}"/>
    <h1>Simple JSF</h1>
    <h:form>
        <ul>
            <li>
                <h:commandLink value="Create" action= "create"/>
            </li>
            <li>
                <h:commandLink value= " View " action= "view"/>
            </li>
        </ul>
    </h:form>
</h:body>
</html>
```

```xhtml
<h:body>
    <h:graphicImage value= "#{resource[’images:logo.png’]}"/>
    <h1>Enter Person Details</h1>
    <h:form>
        <h:messages globalOnly="true"/>
        <p><h:outputLabel for="givenField" value="GivenName:"/>
            <h:inputText id= "givenField" label="GivenName"
                value="#{personBean.given}" 
                required="true"/></p>
        <p><h:outputLabel for="familyField" value="FamilyName:"/>
        <h:inputText id="familyField" label="FamilyName" 
            value="#{personBean.family}" 
            required="true">
            <f:validateLength minimum= "2" maximum= "30"/>
            </h:inputText></p>
        <p><h:outputLabel for="ageField" value="Age:"/>
            <h:inputText id="ageField" label="Age" value= "#{personBean.age}" required="true">
                <f:convertNumber maxFractionDigits="0" maxIntegerDigits= "3" type="number"/> 
            </h:inputText>
            <h:message for= "ageField"/></p>
        <p><h:commandButton action="index" value= "Save"/> </p>
    </h:form>
</h:body>
</html>
```
