---
title: "Application Discovery"
chapter: true
weight: 2
---

# Application Discovery 
Before we begin the modernization process, you must first start to understand the as-is architecture of the system, the technologies being used and their interactions. 

## Understanding the application technologies and size 

Select the application named ***Demo_Express***

You can view the technology breakdown, number of Transactions and Datacall graph.
![Welcome](/images/Sce1-1.png)

## Understand the architecture 

Start by Exploring the Dependencies of the application by Technologies and frameworks.

This positions the view at Level 4 to display the business logic layer, data access layer. 

You can see that the SQL Server database is accessed by the DAO layer, but also by the Business logic layer. 

Position to Level 5 view to display the technology types used with the application. The object nodes are automatically grouped by technology and show the links between technologies including the number of 'sub-nodes' inside the group. 

Another way to drill down from Level 4 view is to double click on the SQL Server Database node to drill down to Level 5 view:


![Screenshot Recipe Level 5](/images/Recipe_Level5.png) 

Recipe is composed of a  
- Presentation Layer with Active Server Pages, JavaScript and HTML, a 
- Logic Layer in C# Classes 
- Data Layer with C# Class DAO with SQL Server Procedures, Tables, Views and Functions 
 
## Modernization scenarios 

Several approaches are considered when migrating an application, 3 scenarios will be covered as part of this workshop: 

- Scenario 1 - you will identify whether the data access layer could be isolated and replaced with a new data access solution (Horizontal partitioning) 

- Scenario 2 - you will consider modernizing the local user authentication by replacing it with a cloud authentication service 

- Scenario 3 - you will create a new logging functionality grouping 