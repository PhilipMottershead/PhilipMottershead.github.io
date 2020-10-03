---
title: "SEM5640 Lecture 5d - JSF Lifecycle"
date: 2020-09-30T13:00:00+0000
categories: [Lecture Notes]
tags: [SEM5640,JavaEE,JSF]
---
* JSF Lifecycle
  * The lifecycle starts with a client request for the URL
  * It ends with the server responding
  * Calls may be
    * The first request in the session
    * A subsequent call - a postback

* First request
  * On the server:
    * facelet is compiled and a component tree generated
    * this is stored in theFacesContext
      * a store object instance
      * one per facelet
    * it is populated with components and managed bean properties with values
    * a view is created
    * the view is rendered
    * the tree is destroyed
    * the view is kept

* Postbacks
  * The user may ask for the same page again
  * The system may ask for it immediately
    * validation or conversion failure
  * the restored view is used again
  * the lifecycle has more stages

* Lifecycle stages
  * Restore View Phase
    * information from the previous call is restored
  * Apply Request Values Phase
    * request parameters are associated with their components
    * any queued events are broadcast to their listeners
  * Process Validations Phase
    * all validators registered on components are executed
    * failures are added to the FacesContext
    * Jump to rendering if there are failures
  * Update Model Values Phase
    * server-side object properties set to values from components
  * Invoke Application Phase
    * application level events, e.g. submitting a form, are processed
  * Render Response Phase
    * delegates to a resource to render the view
    * currently XHTML
