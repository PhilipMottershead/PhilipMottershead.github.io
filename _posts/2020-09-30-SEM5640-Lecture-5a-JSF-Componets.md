---
title: "SEM5640 Lecture 5a - JSF Components"
date: 2020-09-30T10:00:00+0000
categories: [Lecture Notes]
tags: [SEM5640,JavaEE,JSF]
---

## JSF Components

* Build JSF View
* Configurable
* Reusable
* Simple to complex
  * Text input
  * Table
* 5 Elements
  * UI Component classes
    * State and behavior of UI Components
  * A Rendering Model
  * Conversion Model
  * Event/Listener Model
  * Validation Model

## Component classes

* UIComponentBase Extends UIComponent
  * Extended into generic classes
    * UIColumn
    * UIData
    * UIMessages
    * etc...

* Behavior
  * Behavioral interfaces inplemented
  * What they can do
  * Include
    * ActionSource2
      * Fire event
    * StateHolder
      * Hold state
    * ValueHolder
      * Hold local value
    * EditableValueHolder
      * Do Validation
      * fire value change events

* Use
  * Associated tags
  * Built using tags
  * Is open architecture

## Rendering Model

* Component classes define functionality
* How they are rendered in separate class
  * classes have more than one
    * UICommand has 2
      * h:commandButton
      * h:commandLink
* Name indicates function and appearence 
* Each tag has
  * Funtionality in UIComponnet Class
  * Rendering by a rendering class

## Conversion Model

* Associated with Server side data
  * Binding
  * to model
    * uses java data type
* Can have different representation of same data
* Converting strings from HTML components to Java types for     storage
* Standard converters available
  * javax.faces.convert package
    * BigDecimalConverter
    * BigIntegerConverter
    * IntegerConverter
    * etc ...
* custom ones can be built  

* Using converters
  * Bind using managed bean
  * Put in component's converter attribute
  * Nest convert number and dateTime tags
    * f:convertNumber/f:convertDateTime
  * Put f:converter tag
  
## Event/Listener Model

* Strongly typed event classes
* Listener interfaces
* an map HTTP requests to specific handling code
  * listeners, they receive event objects
* Event object identifies the component which fired it and info about
* An implementation of a listener must be registered on the component
* Clicking (using) a component
  * might fire an event
  * might fire an event

* Listeners
  * Listeners cause the application to react to events
    * Implement an event listener class to handle the event
      * register it on the component
    * Implement a method of a managed bean
      * refer to it in an EL method expression attribute in the component tag
  
* Registering listeners on components
* action event
  * Class
    * f:ActionListener
    * type(class name)
    * binding(object)
  * Bean method
    * actionListener
* value-change
  * Class
    * f:valueChangeListener
    * type(class name)
    * binding(object)
  * valueChangedListener
    * valueChanged

* tags go inside the component tag
* one of type or binding is given
* bean method attributes are of the component

* Can do in response
  * Details of component
  * old and new values
  * Access to data in server
    * request
    * session
    * application
    * DB

## Validation Model

* Happens before send to server side model
* Standard validators available
  * set of tags
  * attributes for config
  * tag inside component to register
* Can create own
  * implement validator interface
    * Register with application
    * create tag for it
    * use general f:validator tag
  * Write a managed bean method

* Using validators
  * Error messages
  * register with component
    * Nest tag inside component

* Bean Validation
  * simple
  * access other data
