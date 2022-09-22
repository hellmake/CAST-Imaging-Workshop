---
title: "Modernization scenario 1"
chapter: true
weight: 3
---
## Modernization Scenario 1 - Data Layer separation 

 For the “Recipe” application we have two ways that we could perform data separation :  

“A” : Separate the complete database layer 

We need to ensure that a new platform can host and execute our stored procedures and functions.  

When this is confirmed, "A" seems to be the “easiest” way because it means a change in the DAO configuration only.  

However, it may not be the best long term option as we may want to move the business logic out of the SQL procedures. 

 

“B” : Separate only tables and views 

Create aliases for all the tables and make sure that they are transparent for the stored procedures and functions, or 

modify all the procedures and functions (581 references between Tables/Views and Procedures/Functions). 

 

Either way, there are 3 direct links to the database from the C# Class (in light green), which need investigation. 

![Screenshot Recipe Scenario 1](/images/Recipe_Sce1.png) 

## Investigate dependencies 

As part of the separation planning work, some architectural inconsistencies are discovered. 
For most of the transactions the C# Data Access Object (DAO) is calling stored procedures. The stored procedures are then accessing the SQL Server Tables and Views.  
However, there are 3 references directly between the C# Class and the SQL Server Table.  

Double-click on the edge between C# Class and SQL Server Tables to understand the objects involved. 
We discover it is CalendarSeachProvider.  

Single click on each of the 3 links (dotted edges) and see that the same C# Method is involved in those 3 references. 

Double click on either of those 3 dotted edges to display the details. 

Double click on the edge between CalendarSearchParam and the SQL Server Table to display the source code. 

(another way is to Right-click on CalendarSearchProvider to Show Source Code and read the source code for the method CalendarSearchParam) 

 

The source code reveal a single SQL select accessing the 3 SQL Server Tables. This SQL should be in a SQL Server Procedure. 

![Screenshot Recipe Scenario 1 code viewer](/images/Recipe_Sce1Code.png) 

## Create an action plan 

  

Close the current view to go back to the 4 objects in question : CalendarSearchParam and the 3 SQL Server tables. 

Use the left menu button “Export all Object and Links” to extract the list of objects on the current view in an Excel report. 

Note that you also have prepared reports in the left menu "Reports":
![Screenshot Recipe Scenario 1 report](/images/Recipe_Sce1Rep.png) 