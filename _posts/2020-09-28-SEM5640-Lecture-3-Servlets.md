---
title: "SEM5640 Lecture 3 - Servlets"
date: 2020-09-28T15:00:00+0000
categories: [Lecture Notes]
tags: [SEM5640,JavaEE]
---
## Servlets

* Core EE web Component tech
  * Used alone as well as a build block
  * Many more complex tech is built on top of servlets

* Dynamic Page
  * Has URL
  * Receives HTTP request
    * Method
    * Header
    * Query Parameter
    * Body
  * Send Response
    * Response code
    * Header
    * Body
* Servlet Class
  * Manages Lifecycle
  * Extends java.servlet.HTTP.HTTPServlet.class
  * First call
    * Load Class
    * Create instance
    * init()
  * Any Call
    * Handle HTTP Request
  * Destroy() can be overridden
  * Server only needs on instance of the servlet
  
* Building a servlet
  * Extends HTTPServlet
    * Does nothing
    * Is a Abstract Class
  * Override methods
    * init()
    * destroy()
    * requests

* Handling requests
  * Service Methods
  * has one per HTTP method
    * doGet()
    * doPost()
    * finds http type
    * override if you want functionality  
    * doGet and doPost commonly use the same method

```java
protected void doGet(HttpServletRequest request,
                HttpServletResponse response)
                throws ServletException, IJavaEE
protected void doPost(HttpServletRequest request,
                HttpServletResponse response)
                throws ServletException, IOException{
    processRequest(request,response);
}
```

```java
protected void processRequest(HttpServletRequest request,
                            HttpServletResponse response)
                            throwsServletException, IOException{
    response.setContentType("text/html;charset=UTF−8");
    try(PrintWriter out = response.getWriter()) {
        out.println("<html >");
        out.println("<head>");
        out.println("<title>Servlet Time</title>");
        out.println("</head>");
        out.println("<body>");
        out.println("<h1> Servlet Time </h1>");
        out.println("<p>Use of try −with−resources construct </p>");
        Date now = new Date();
        out.println("<p>" + now.toString() + "</p>");
        out.println("</body>") ;
        out.println("</html>") ;
    }
}
```

* Set a header
  * setContentType is a specialised method
* Get a writer from the response object
* Use arbitrary Java
* Remember to close the writer

* Request
  * Provides access to:
    * Call details
    * Parameters
    * Body
    * A Reader
    * Context
* Response
  * Provides access to:
    * Response code
    * Headers
    * A writer (for the body)

## Accessing details of the call

* HttpServletRequest, HttpServletResponse
  * Passed as parameters
* HttpServletRequest provides access (getters and parsers) to
  * HTTP headersJavaEE
  * HTTP parameters (GET and POST)
  * The request body
  * multipart/form-data - input stream for file upload
  * Other HTTP packet data
  * Attributes q.v.
  * Session q.v.
* It extends javax.servlet.ServletRequest
  * inheriting many access methods more general than HTTP

## Forwarding

* A servlet performs some logic and forwards the request to another
  * With request and response objects
* “Branching” on context
* First servlet outputs nothing
* Range of uses (q.v.)

```java
RequestDispatcher dispatcher =
request.getRequestDispatcher("ShowRequest");
dispatcher.forward(request,response);
```

## Data

* A servlet could have instance variables
* There is only one instance of a servlet
  * (probably, we must believe)
* Multiple users would see the same values
* Is that what we want?
* But how do we know which user is which
  * HTTP?

[Code for examples can be found here](https://github.com/PhilipMottershead/SEM5620_Servlets)