---
title: "SEM5640 Lecture 4 - Dotnet Intro"
date: 2020-09-29T10:00:00+0000
categories: [Lecture Notes]
tags: [SEM5640,Dotnet]
---

* What is .NET?
  * Microsoft’s framework for developing and deploying applications
  * Cloud (Azure)
  * Web Server
  * Desktop
  * Mobile Phones (and experimented with other restricted devices
* Similarities with the Java Runtime Environment
* Historically, this has been focused on Windows
* Microsoft has developed .NET Core, which is now at version 3 (version 5 is close to release)

![Dotnet](/assets/img/dotnet.png "Dotnet Diagram")
![Java](/assets/img/java.png "Java Diagram")

## Multiple Development Languages

* Application can be written in any .NET compliant language•
  * C#
  * Visual Basic .NET (VB.NET)
  * F#
  * Managed C++
* Others...
  * Cobol
  * Python
* Natural fit for Object Oriented languages
* All languages compile to Microsoft Intermediate Language (MSIL)
  * managed code
  * Interoperability between modules written in different languages
* Common Type System (CTS)
* Common Language Specification (CLS)

## Common Language Runtime

* Loads and executes .NET managed code in the form of assemblies
* CLR loads code into Application Domains
  * Level of isolation
  * Ability to stop and remove a domain
* JIT Compilation•Memory Management with Garbage Collection
* Manages Security

## .NET Framework and .NET Core

* Microsoft introduced .NET Core a few years ago
* .NET Framework represents the long term investment in the .NET platform, focused on Windows devices
  * There were 3rd party efforts to take .NET to other platforms
* .NET Core is a version of .NET that is designed to work across platforms (Windows, Linux and macOS). 
* .NET Core doesn’t include everything from .NET Framework
  * Focus on cross-platform deployment and can be used for IoT and cloud.
* .NET Core 2 and later supports C#, Visual Basic.NET and F#

![Dotnet Core](/assets/img/dotnetcore.png "Dotnet Core Diagram")
![Compile-Execute Cycle](/assets/img/Compile-Execute.png "Compile-Execute Cycle")

[Code for examples can be found here](https://github.com/PhilipMottershead/SEM5640_dotnet_Workshop1)

## ASP.Net

* A brief history
* ASP.NET WebForms
  * A visual form is created, such as that on a desktop machine
  * The application manages state, including state of the view between each page access
  * Tries to behave more like a desktop application, reducing the work that a developer needs to do on each page refresh. 
  * Lots of controls available and easy to create re-usable code
* ASP.NET MVC was introduced -several versions up to MVC 5
* ASP.NET MVC Core is latest version of MVC
* .NET Core has also added:
  * Razor Pages –closer to ideas in WebForms
  * Blazor-using Web Assembly

## ASP.NET MVC

* Model, View, Controller design pattern
* Removes the abstraction of the “desktop application” that exists in WebForms•Separation of the View from the Controller
* Choice of how you implement the Model, although you get a lot of support with the Entity Framework
* Convention over configuration
