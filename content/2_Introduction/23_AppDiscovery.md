---
title: "Application Discovery"
chapter: true
weight: 3
---

# Application Discovery 

**Objective**: Before you begin the modernization process, you must first understand the as-is architecture of the system and understand: Which are the technologies being used? How do they interact? Are there isolated layers which code is not referenced? What are the frameworks in place and are they compatible with the target platform? etc. 

## The applications we'll walk through

For the purposes of this workshop, we are going to discover 2 applications: one of them is a Java/MySQL online store application and the other one is a .NET-based cooking recipes management webapp.

## Understanding the application technologies and size 

Select the application named ***eCommerce***.
Information on the application size, number of lines of code, number of objects, etc. are displayed along with several navigation scenarios to drill-down and discover the application and its dependencies.

![Welcome](/images/eCommerce_welcome.png)

Choose the ***Application Architecture*** scenario to explore the objects composing this application grouped by technology types. You can drill down in the different levels of abstraction describing the several layers of the application architecture:  

- Level 3: you learn about the services and coordination layers in place and their interaction 
- Level 4: you can see all the technologies and frameworks composing the application and understand how the Business Logic is accessing the Database Layer, what composes the Presentation Layer, and the architecture specifics (batches, coordination layers, legacy frameworks, etc.) 
- Level 5: the object types are displayed: this is the lowest level of visualization for this view. You can see the number of low level components inside each node (classes, tables, pages, etc.)

![eCommerce Overview](/images/eCommerce_level3.png)

## Understanding the architecture 

Choose the Level 5 of the navigation perspective. You see that *eCommerce* is composed of a UI layer in JSP and Javascript. Struts and Hibernate are also in use with a MySQL database. 

![eCommerce Level 5](/images/eCommerce_level5.png) 

CAST Imaging provides navigation capabilities to help you understand the inner architecture of the application and answer questions such as: 
- Which are the JSP pages still using Struts? 
- How is the MySQL data consumed? 
- The *Log4j* component requires an urgent upgrade due to a security vulnerability. Which components would be impacted by this upgrade? 

{{% notice tip %}}
You can change the Graph Layout to ***Hierarchical*** or ***Force*** to have a better display.\
You can double click on the edge between two nodes to visualize the detailed references.\
You can double click on the node itself to visualize the sub-nodes and explore the dependencies.
{{% /notice %}}

Double-click on the ***API Apache Log4j*** node. On the left-hand menu, you can change the ***Drill Down Options*** to ***Children + caller/callee*** to visualize the Log4J classes and their direct callers/callees.  
 ![Log4j investigation](/images/eCommerce_log4j.png)
 
## The Recipe Application

Now select the application named ***Recipe*** and apply the same navigation steps than above.
 ![Screenshot Recipe Level 5](/images/Recipe_Level5.png)

You understand rapidly the high level characteristics of ***Recipe*** application:
- Presentation Layer with Active Server Pages, JavaScript and HTML
- Logic Layer in C# Classes
- Data Layer with C# Class DAO with SQL Server Procedures, Tables, Views and Functions
- Among the APIs used in the application, we see .NET System Diagnostics Logging framework
- The SQL Server tables are accessed by C# but also by SQL Server Procedures, which is not a recommended architecture design to ensure database integrity. 

But are those SQL Server Procedures really used by the C# layer ?
Right click on the node *SQL Server Procedures* > *Children+caller/callee* to identify the adherence with the C# Classes.
![Screenshot Recipe Level 5](/images/Recipe_SQLProc.png)
 
You now see the all the callers and callees of the SQL Server Procedures grouped by object type: C# Classes, SQL Server Functions, SQL Server Tables, and SQL Server Views.

Now hide the type *SQL Server Tables* in the right hand legend to render a more readable view: you see only a few SQL Server Procedures that show no references to neither SQL Server Functions nor C# Classes. 

:memo: This confirms that the SQL Server Procedures are really used by the C# layer, the code they contain needs to be maintained.

![Screenshot Recipe Level 5](/images/Recipe_SQLProcDetails.png)

**You now have, rapidly in a few clicks, gathered valuable insights on the applications:** 
- Source Code size and list of frameworks
- Technologies involved and how they interact
- Data Layer consumption mechanisms
- Architecture Design hurdles (layer bypass, uncompliant design)

**This will help you to move on to the next step of the journey and study several modernization scenarios.**

Close the view to get back to the Level 5 perspective and prepare for the next exercise.

![Screenshot Recipe Level 5](/images/Recipe_closeview.png)