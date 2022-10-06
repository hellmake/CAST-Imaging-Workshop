---
title: "Data Layer Separation"
chapter: true
weight: 1
---

# Separate the Data Layer towards AWS Storage

**Objective** : With the goal to integrate an AWS Storage solution, we plan to separate the data layer from the implementation layer. 
After separation, the database could be hosted on AWS RDS platform. A more advanced scenario would be to use AWS Database Migration Service to migrate the whole SQL Server database on AWS Aurora.

But how to estimate the feasibility and effort of those scenarios ? What are the technical prerequisites before engaging in such transformation ?

## Identify the architecture constraints

Exploring application ***Recipe*** at the Layer 5 perspective, you will investigate the links between SQL Server data layer and C# Classes.
We have two options to achieve a data layer separation :  

**A** – Separate the complete database layer. We need to ensure that a new platform can host and execute our stored procedures and functions. 
**A** seems to be the “easiest” option, however, it may not be the best long term option as we may want to move the business logic out of stored procedures that are difficult to maintain. 

**B** – Separate only tables and views and leave the stored procedures for later. This requires to create aliases for the tables in the meantime and make sure that they are transparent for the stored procedures and functions. Option **B** involves a transformation in two steps : first the tables, then the code. CAST Imaging shows 581 references between Tables, Views, Procedures, Functions, hence creating table aliases including the testing phase represents a non negligeable workload. 

:memo: Either way, a technical prerequisite is to remove bypass towards the SQL Server Tables (in light green below) : 
- 3 references to the tables from the C# Class bypassing the C# DAO Layer 
- 3 references from C# Class DAO directly to the tables, bypassing the SQL Server Procedures 

![Screenshot Recipe Data Access Layer](/images/Recipe_Sce1_data.png) 

## Investigate dependencies 

:memo: As part of the separation planning work, you have discovered some architectural inconsistencies. For most of the transactions, the C# DAO is calling SQL Server procedures which are then accessing the SQL Server Tables and Views. However, there are direct references bypassing the DAO layer and the SQL Server Procedures. 

Double-click on the edge between C# Class and SQL Server Tables to understand the objects involved. 
You discover a method *CalendarSearchParam* pertaining to the class *CalendarSeachProvider*.  

![Screenshot Recipe Bypassing DAO references](/images/Recipe_Sce1_method.png) 

Now, right click on either of those 3 edges to display the source code.

:memo: The source code reveals a single SQL SELECT statement accessing the 3 SQL Server Tables : this statement should be in a SQL Server Procedure. 

![Screenshot Recipe Bypassing DAO code viewer](/images/Recipe_Sce1_code.png) 

## Create an action plan 

Now, there are several actions in CAST Imaging to share what you observed and report the action items decided : 

### Save the view

{{% notice info %}}
You can save a view in CAST Imaging by clicking on *Save a View* in the left hand menu. This allows you to retrieve, modify, document the view later on.
The saved views are visible to all CAST Imaging users of the same application and appear in the properties of all nodes contained in the saved view.
{{% /notice %}}

![Screenshot Recipe Bypassing DAO code viewer](/images/Save.png) 
You can display the views saved previously from the left hand Menu Bar.
![Screenshot Recipe Bypassing DAO code viewer](/images/SavedViews.png) 


### Document the view

{{% notice info %}}
You can save your observations on a view in CAST Imaging for other team members to rapidly understand the situation.
This allows to display a note whenever the selected nodes will be displayed on the screen, and it also allows to search by *Document* name and retrieve those nodes later on.
{{% /notice %}}

Select the method, the class and the 3 SQL Server tables and add a *Document-IT* resuming the situation that you observed. 

![Screenshot Recipe Bypassing DAO code viewer](/images/DocumentIT.png)
You can view the *Documents* attached to a node by clicking on the bottom note appearing when the node is on the screen.
![Screenshot Recipe Bypassing DAO code viewer](/images/DocumentIT_click.png)

### Export the view

{{% notice info %}}
You can export the metadata contained in a view to several formats (CSV, Excel, JSON, JPG, SVG).
{{% /notice %}}

Use the left menu button *Export all Object and Links* to extract the list of components and information on the references between them in an Excel report. 
![Screenshot Recipe Scenario 1 report](/images/ExportObjectsandLinks.png) 