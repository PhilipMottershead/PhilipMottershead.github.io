---
title: "SEM5640 Lecture 5a - JSF Component Libraries"
date: 2020-09-30T11:00:00+0000
categories: [Lecture Notes]
tags: [SEM5640,JavaEE,JSF]
---

* Component Libraries (Tag Libraries)

* New components can be built
  * Java, XML

* Commercial and Open Source libraries available
* More sophistiocated UI components
  * Trees
  * Charts
  * Drag and Drop

* Richfaces
  * <http://showcase.richfaces.org>
* ICEfaces
  * <http://www.icesoft.org/java/projects/ICEfaces/overview.jsf>

## Tag libraries in facelets

* JavaServer Faces HTML Tag Library
  * <http://xmlns.jcp.org/jsf/html>
  * components
  * h:head h:body h:outputText h:inputText
* JavaServer Faces Facelets Tag Library
  * <http://xmlns.jcp.org/jsf/facelets>
  * ui:
  * templating
  * ui:component ui:insert
* JavaServer Faces Core Tag Library
  * <http://xmlns.jcp.org/jsf/core>
  * f:
  * custom actions
  * f:actionListener f:attribute
* JSTL Core Tag Library
  * <http://xmlns.jcp.org/jsp/jstl/core>
  * c:
  * include flow controlID
  * c:forEach
* JSTL Functions Tag Library
  * <http://xmlns.jcp.org/jsp/jstl/linebreakfunctions>
  * fn:
  * functions
  * fn:toUpperCase

## The Expression Language

* Communication between
  * the presentation layer (View) in JSF (JSP)
  * the application logic (Model) in Managed Beans
* Page authors can dynamically access data from JavaBeans components
  * in the web tier
  * in the business tier
* EL can
  * dynamically read application data stored in JavaBeans
  * dynamically write data, such as user input into forms
  * invoke static and public methods
  * dynamically perform arithmetic operations

* Always in {. . . } brackets
  * ${...}
    * immediate evaluation
    * when page is generated
    * read only
  * #{...}
    * deferred evaluation
    * at any point in the page lifecycle
    * value expressions – read and write
    * method expressions

* can be rvalue (read only) or lvalue (read/write)
* Can refer to objects and attributes
  * Compponets
  * collections
  * java enum
* an object is searched for
  * in the page, request, session, and application scopes
  * in that order
  * (can be customised)
* object properties are referenced with “.” or “[’name’]”
  * #{customer.name}or#{customer["name"]}
    * single or double quotes
  * arrays or lists use an int
    * #{customer.orders[1]}
* a map can be accessed by string literal
  * #{customer.orders["socks"]}
* an rvalue can be literals or use operators
  * ${42} ${"hello"} ${myobject.length + 10}
  * standard set of operators available
  * rvalues can be used anywhere, including static text
* lvalues can only be used in tag attributes which allow them
  * intuitive whether they are r or l
* can be concatenated
  * <another:tagvalue="some#{expr}#{expr}text#{expr}"/>

* Method Expressions
  * always deferred
  * can use “.” or “[]”
    * #{myBean.method1} #{myBean["method1"]}
  * can only be used in tag attributes
    * with a single expression construct (not concatenated)
      * <a:tag value="#{bean.method}"
    * or as just text
      * support for navigation
      * a method can return a string
      * or it’s a literal

* Reserved words
  * and or not eq ne lt gt le ge true false null instanceof empty div mod