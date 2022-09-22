---
title: "Modernization Scenario 4"
chapter: true
weight: 5
---
# Modernization Scenario 4 - Creating a Logging Functional Grouping  

##Prerequisite 


Continue your journey to CAST Imaging features detailing the aggregation feature here 

Link to CAST-U course on search  
 

## Regroup objects that will be transformed to visualize the adherence 

For this scenario using “Recipe” we’ll create a grouping of functionality that accesses the log tables within the database.  

Using the “Recipe” application, select “Custom Aggregation” from the top right
![Custom Aggregation](/images/Recipe-CustomAgg.png)

This will take you into the custom aggregation view.  

Custom aggregation allows you to create custom nodes by aggregating the application objects. This allows to visualize the adherence with the rest of the application objects to prepare the TO-BE architecture or to identify gaps or strong coupling between functional groups. 

Custom aggregation can be published to be shared with the application team for contribution. 

 

Select “Create new aggregation view”, that you can name freely. Populate the aggregation using “Module”. 

The aggregation is them pre-populated with a list of Modules representing the main functional groups in the application. 

 

Publishing the custom aggregation will make it visible with all. 

Users can modify the aggregation view from other views or from within the Custom Aggregation Menu. 

 

For this scenario exit the custom aggregation view and return to the standard view. 

In this application, the logs are contained in SQL Server database. Search for the "log" tables using the “Search” and narrow down the search to objects of type “SQL Server Tables”.  

“Visualize” the 5 SQL Server Tables and select them all. 

Right-click on all the tables and select “Add callers”  

Among the objects on the view, you can see SQL Server Procedures, Primary keys.  

Select the objects which names refer to "Log" or "Error" 

 

Right-click on all of them and select “Associate to custom aggregation” 

Select the name of the custom aggregation that you created earlier and then select a “New custom node” and name it. 

Make sure to check the box "Remove objects from other existing nodes" 

Click the “Associate” button to add the functionality grouping to the custom aggregation 

![Custom View](/images/Recipe-CustomView.png)

Refresh the Imaging page, then 

In the Left hand Menu, change the SCOPE to Application, and the "AGGREGATED By" to the Aggregation that you created earlier. 

The new functional grouping will be displayed. You can now visuaize the adherence of the application with the Log Tables and their callers, which will help you identify which components to modify when replacing this custom Log layer by a Cloud Logging Service such as AWS CloudWatch. 
![Custom View](/images/Recipe_AggregationResult.png)
