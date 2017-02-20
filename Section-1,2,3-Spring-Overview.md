# Introduction

## Spring Overview

### Introduction
* Very popular framework for building Java applications 
* Initially a simpler and lightweight alternative to J2EE

### Spring Framework Overview
* Core container: the heart of it for creating beans 
  * Context: the Spring container that holds the beans in memory
* Infrastructure: To add services like Security and transcations to your webapp
* Data Access Layer: To interact with databases. We have a number of good helper classes for JDBC and JMS
  * ORM: Object related mapping to hook up to other frameworks like Hibernate
  * JMS: To write to queues in an asynchronous fashion
* Web Layer: Home for the Spring MVC framework. Can use struts and other frameworks
* Test Layer: Extensive support for Test Driven Development
  * Integration: You can create application contexts and wire up your desired objects 

### Spring Projects
A number of projects that are built on top of the core Spring Network   
You use what you need  
Available on spring.io  

* Spring Security
* Spring for Android
* Spring Boot: very popular
* Spring Social: For integrating with 
* Spring Web Services for Rest and SOAP

## Setting up your Development Environment

### Initial Setup
* Install a JDK, Tomcat 8.0 and Eclipse EE edition  
* Go to servers tab at the bottom of Eclipse and click add new server
* Select the unzipped Tomcat server

### Downloading Spring JAR Files
#### Creating a new Eclipse Project
* File -> New Java Project -> Give it the name
* Create a new folder in your eclipse folder called lib

#### Setting up the libraries
* Download the zip for Spring Jar from the latest release at: http://repo.spring.io/release/org/springframework/spring/
* Extract the zip, go to lib and copy all the JAR files from there to the lib folder in Eclipse
* Download the zip for Apache Commons Logging from the latest release at: https://commons.apache.org/proper/commons-logging/download_logging.cgi
  * Spring depends on this library
* Extract the JAR file (commons-logging) from there to the lib folder in Eclipse

#### Adding the libraries to the Project Class Path
* Right Click the project name -> Properties -> Java Build Path -> Libraries -> Add JARs -> and select all the JARs you added
* You should be able to see the JARs in a new Eclipse Folder called Referenced Libraries

### Spring Container
The Spring Container provides an object factory which handles:
* Inversion of Control (Section 4)
* Dependency Injection (Section 5)

There are 3 ways of configuring the Spring Container
* XML configuration file (legacy, but most legacy apps still use this) - Section 4 and 5  
* Java Annotations (modern) - Section 7,8 and 9
* Java Source Code (modern) - Section 10
