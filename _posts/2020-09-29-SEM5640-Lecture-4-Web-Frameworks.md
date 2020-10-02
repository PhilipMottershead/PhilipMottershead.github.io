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
![JSF Diagram](/assets/img/jsf.png "JSF Diagram")

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

## index.xhtml

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

* XHTML (transitional)
* tags from two sets:
  * [XHTML](http://www.w3.org/1999/xhtml) – standard XHTML
  * [JSF](http://java.sun.com/jsf/html) – JSF version, h namespace
* some XHTML are “mirrored” by jsf/html elements
  * jsf/html versions are components
    * added functionality
    * processed by the servlet
* some jsf/html tags are not in XHTML
  * e.g. h:graphicImage
* the value attribute value has odd syntax
  * Expression language (EL)
  * Access to Java
* XHTML can be used
  * some tags not available in jsf/html space
  * passed through to output

## create.xhtml

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
            <h:inputText id="ageField" label="Age"
                    value= "#{personBean.age}"
                    required="true">
                <f:convertNumber maxFractionDigits="0"
                    maxIntegerDigits= "3"
                    type="number"/>
            </h:inputText>
            <h:message for= "ageField"/></p>
        <p><h:commandButton action="index" value= "Save"/> </p>
    </h:form>
</h:body>
</html>
```

* collecting information
* much of the page is in an h:form
  * more powerful than XHTML \<form>
  * does not require action and method (framework provided)
* h:messages causes display of validation or conversion errors
  * for all components
  * h:message can be associated with one component
* h:outputLabel associated with an input (for non-graphical rendering)
* inputText has a label attribute for error reporting
* required is a validation check
* f:validateLength is a built-in special validation check
* all 3 inputs have a value
  * set by EL
  * remembered between displays
    * error reporting
    * but actually any re-display
  * stored in a Java Bean (an instance of a class)
* <h:induct id="ageField" has a converter
  * built in
* h:commandButton will submit
  * action attribute is “what to do next”
    * evaluate to a string, which determines next page
    * defaults to a .xhtml page of that name

## JSF components

* Html equivalents
  * image - graphicImage
  * link - commandLink
  * form - form
    * Links JSF to code
  * input - inputText
  * text - OutputLabel
* Attributes
  * required - Validates a input is entered
  * convertNumber - coverts a input into number and can do validation on these numbers
  * validateLength - Validates length of input

## View Snippet

```xhtml
<html xmlns="http://www.w3.org/1999/xhtml"
  xmlns:h="http://java.sun.com/jsf/html">
  <h:head>
    <title>FaceletTitle</title>
  </h:head>
  <h:body>
    <h:graphicImage value="#{resource[’images:logo.png’]}"/>
    <h1>View Person Details </h1>
    <h:panelGrid columns= " 2 " >
      <h:outputText value="Given name: "/>
      <h:outputText value="#{personBean.given}"/>
      <h:outputText value="Family name: "/>
      <h:outputText value="#{personBean.family}"/>
      <h:outputText value="Age : "/>
      <h:outputText value="#{personBean.age}"/>
      #{personBean.given}
    </h:panelGrid>
    <h:form>
      <h:commandButton value="Home" action="index"/>
    </h:form>
  </h:body>
</html>
```

* the EL can access the same Java Bean instance
  * Can Access Backing Beans
  * Managed by Web Containers
  * Accessible Anywhere in context

## Bean Snippet

```java
@ManagedBean
@SessionScoped
public class personBean implements Serializable {
  public personBean ( ) {
  }
  private String given ;
  / ∗∗
  ∗ Get the value of given
  ∗
  ∗ @return the value of given
  ∗ /
  public String getGiven ( ) {
    return given;
  }
  / ∗∗
  ∗ Set the value of given
  ∗
  ∗ @param given new value of given
  ∗ /
  public void setGiven (String given){
    this.given = given;
  }
```

* Annotated
  * @Named
    * Accessible by the EE
    * Managed by container
  * @Session Scoped
    * Controls Scope
    * @RequestScope
    * @ApplicationScope
  * Contains a set of Attributes

[Link to Workshop 1 code](https://github.com/PhilipMottershead/SEM5640-JavaEE-Workshop1)
