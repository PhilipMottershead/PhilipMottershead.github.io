---
title: "SEM5640 Lecture 3a - Session"
date: 2020-09-28T15:00:00+0000
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
void removeAttribute(String name)
```

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
