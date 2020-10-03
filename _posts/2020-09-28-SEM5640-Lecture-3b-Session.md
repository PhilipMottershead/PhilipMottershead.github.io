---
title: "SEM5640 Lecture 3b - Session"
date: 2020-09-28T16:00:00+0000
categories: [Lecture Notes]
tags: [SEM5640]
---
## HTTP

* HTTP
  * Request -Response
    * client request (parameters)
    * Server response
    * Next request is unconnected
    * parameters can't add to requests
    * User?
    * Stateless  

## States

* State
  * Users Assume requests are connected.
  * Need state to allow this
  * Provider wants to connect behavior
    * normally though login
    * Building profile

* Keeping State
  * Memory
  * Files
  * DBMS

## JavaEE Sessions

* The HttpServletRequest has a method
  * HttpSession getSession()
* On first request
  * Session is created
  * New identity is returned
* On Further Requests
  * Identity is looked up
* Can store user data

### JavaEE session tracking

* Defaults to cookies
  * code needs to specifically support attributes
  * using response.encodeURL(URL)

### Session Attributes

* Obtain from request
* Has Set and Get methods
* This where session data is stored
  * Can be any type
  * Accessible by any servlet in session

## Examples

## index.html session

```html
<ul>
  <li><a href="Ident">Identity</a></li>
</ul>
<h2 id="session">Session</h2>
<ul>
  <li>
    <a href="SetMake">Set make</a>
  </li>
  <li>
    <a href="ShowMake">Show make</a>
  </li>
```

## Show Make

```java
protected void processRequest(HttpServletRequest request,
        HttpServletResponse response)
        throws ServletException, IOException {
  response.setContentType("text/html;charset=UTF-8");
  PrintWriter out = response.getWriter();
  try {
    out.println("<html>"); out.println("<head>");
    out.println("<title>User</title>");
    out.println("</head>"); out.println("<body>");
    out.println("<h1>User</h1>");
    String u = (String) request.getSession().getAttribute("make");
    if (u == null) {u = "";}
    out.println("<p>Current make: " + u + "</p>");
    out.println("<p><a href='index.html#session'>"
            + "Home</a></p>");
    out.println("</body>");  out.println("</html>");
  } finally {
    out.close();
  }
}
```  

## Set Make

```java
protected void processRequest(HttpServletRequest request,
                              HttpServletResponse response)
        throws ServletException, IOException {
  HttpSession sesh = request.getSession();
  String themake = request.getParameter("mymake");

  if (themake == null || themake.isEmpty()) {
    response.sendRedirect("setmake.html");
  } else {
    sesh.setAttribute("make", themake);
    request.getRequestDispatcher("ShowMake").forward(request,
                                                    response);
  }
}
```

### Ending a session

* Sessions will expire with cookies
* Can be terminated by the server
* HttpSession has an invalidate() method

```java
protected void processRequest(HttpServletRequest request,
        HttpServletResponse response)
        throws ServletException, IOException {
  request.getSession().invalidate();
  RequestDispatcher dispatcher;
  dispatcher = request.getRequestDispatcher("index.html");
  dispatcher.forward (request, response );
}
```

### Handling Session Attributes

```java
void setAttribute(String name, Object value)
Object getAttribute (String name)
Enumeration <String> getAttributeNames()
void removeAttribute(String ---
title: "SEM5640 Lecture 4a - Servlets"
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
}---
title: "SEM5640 Lecture 4a - Servlets"
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
## Other Attributes

* Attributes are objects of any class
* Associated with session
* Also with
  * Servlet Context (running application in a server)
  * Request
* set and get methods for them
* Name/object pairs

### Servlet Context

* For the life of the running application
* Across all requests and sessions
* ServletRequest (supertype of HttpServletRequest) has a method

```java
ServletContext getServletContext ()
```

This has attributes
Accessible from servlets

```java
ServletContext servletContext = getServletContext ( ) ;
X x = new X();
servletContext.setAttribute("myX" ,x);
X x = (X) servletContext.getAttribute("myX");
```

Attributes available in all sessions from all servlets

### Request Attributes

* the HttpServletRequest has attributes
  * inherited from ServletRequest
* No storage between requests
* Used when passing on a request

### Request attribute and forwarding

* The servlet Page is available at URL Choice

```java
@WebServlet(name = "Choice", urlPatterns = {"/Choice"})
public class Page extends HttpServlet{
```

* It adds request attributes based on the query string received
* And forwards to ShowRequest again
  
```html
 <li>
    <a href="Logoff">Logoff</a>
  </li>
</ul>
```

## Page

```java
protected void processRequest(HttpServletRequest request,
                              HttpServletResponse response)
        throws ServletException, IOException {
  ArrayList<String> data = new ArrayList<String>();
  String choice = request.getParameter("direction");
  if (choice.equals("left")) {
    data.add("bent");
    data.add("broad");
  } else if (choice.equals("right")) {
    data.add("straight");   data.add("narrow");
  } else {
    throw new ServletException("Unexpected option");
  }
  request.setAttribute("myattribute", data);
  RequestDispatcher dispatcher =
    request.getRequestDispatcher("ShowRequest");
  dispatcher.forward(request, response);
}
```

## Error handling

```xml
<error-page>
  <error-code>404</error-code>
  <location>/MissingPage.html</location>
</error-page>
```

[Code for examples can be found here](https://github.com/PhilipMottershead/SEM5620_Servlets)
