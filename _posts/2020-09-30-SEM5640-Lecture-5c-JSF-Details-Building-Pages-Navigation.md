---
title: "SEM5640 Lecture 5c - JSF Building-Pages-Navigation"
date: 2020-09-30T12:00:00+0000
categories: [Lecture Notes]
tags: [SEM5640,JavaEE,JSF]
---
## Building pages

* Attributed
  * id
  * Style
    * link to css
  * rendered
    * boolean
    * can be set via EL
  * value
    * value of component
      * Set via EL

* Input tags
  * h:inputText – one line
  * h:inputSecret – asterisks
  * h:inputTextarea – multiple line
    * Attributes
    * converter – a converter to use converter
    * Message – for when conversion fails
    * label
    * lang
    * required – validation
    * requiredMessage
    * validator – method expression
    * validatorMessage
    * valueChangeListener – method expression

```xhtml
<h:inputText id="name"
    label="Customer Name"
    size="30"
    value="#{cashierBean.name}"
    required="true"
    requiredMessage="#{bundle.ReqCustomerName}">
    <f:valueChangeListener
        type="dukesbookstore.listeners.NameChanged"/>
</h:inputText>
```

* Output tags
  * :outputText – one line
  * h:outputLabel – read only
  * h:outputLink – simple hyperlink, no action

* Actions and Navigation
  * h:commandButton– a button
  * h:commandLink– an HTML link
    * must have ah:outputText inside
  * must have one of the attributes
    * action– string or string method expression
      * determines next page
    * actionListener– method expression
      * process the action event
  
```xhtml
<h:commandButton value="Submit"
                 action="#{cashierBean.submit}"/>

```xhtml
<h:commandLink id="Duke" action="bookstore">
    <f:actionListener
        type="dukesbookstore.listeners.LinkBookChangeListener"/>
    <h:outputText value="#{bundle.Book201}"/>
</h:commandLink>
```

* Layout
* h:panelGrid
* h:panelGroup
* generates an HTML table
  * poor practice
  * not how to display data
  * h:dataTable
  * tags for header, footer, body, rows

* Selecting one value
  * h:selectBooleanCheckbox
  * h:selectOneRadio
  * h:selectOneMenu
  * h:selectOneListbox
  
```xhtml
<h:selectOneMenu id="shippingOption"
    required="true"
    value="#{cashierBean.shippingOption">
    <f:selectItem itemValue="2" itemLabel="#{bundle.QuickShip}"/>
    <f:selectItem itemValue="5" itemLabel="#{bundle.NormalShip}"/>
    <f:selectItem itemValue="7" itemLabel="#{bundle.SaverShip}"/>
</h:selectOneMenu>
```

```xhtml
<h:selectManyCheckbox id="newslettercheckbox"
    layout="pageDirection"
    value="#{cashierBean.newsletters}">
    <f:selectItems value="#{cashierBean.newsletterItems}"/>
</h:selectManyCheckbox>
```

* Composite components
  * built from standard components
  * parameterized
  * stored in resources
    * has a namespace
    * http://xmlns.jcp.org/jsf/composite/ezcomp

* JSF templates
  * A facelet using tags from:
    * <http://xmlns.jcp.org/jsf/facelets> namespace (ui:)
  * Other pages are built based on it
    * client pages
  * The template leaves slots
    * \<ui:insert name="top">Top Section</ui:insert>
  * The client calls on a template
    * \<ui:composition template="./template.xhtml">
  * and fills in named slots

```xhtml
 <ui:define name="top">
    Welcome to Template Client Page
</ui:define>
```

## Navigation

* Rules in a configuration file
  * typically faces-config.xml
* Rules written in XML
* Each rule is for a page (called view)
* For a page there is a set of outcome - strings
* For each outcome, a next page is specified

```xml
<navigation−rule>
    <description>Navigation from homepage</description>
    <from−view−id>index.xhtml</from−view−id>
    <navigation−case>
        <from−outcome>doCreate</from−outcome>
        <to−view−id>create.xhtml</to−view−id></navigation−case>
    <navigation−case>
        <from−outcome>doView</from−outcome>
        <to−view−id>view.xhtml</to−view−id>
    </navigation−case>
</navigation−rule>
```

* Generating outcomes
  * Components may have action attributes
  * These can have string values – the outcomes
    * \<h:commandButton id="submit" action="doCreate"value="Submit" />
  * action attributes can use EL to reference a managed bean method
    * must take no parameters and return a String
    * the string is the outcome

* Implicit Navigation Rules
  * When no rule can be found
  * JSF will look for a matching page
  * \<h:commandButton value="submit" action="response">
  * if no rule for response for the current page is found
  * look for response.xhtml
