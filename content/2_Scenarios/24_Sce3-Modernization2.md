# Modernization Scenario 3 - Replacing authentication 

 

##Prerequisite 

 

Continue your journey to CAST Imaging features detailing the search feature here 

Link to CAST-U course on : Enriching and searching views and objects  

 

## Search for objects to be replaced 

Ecommerce application uses an application specific authentication which we would like to replace with a cloud authentication. 

 

Start by “Searching” for the database tables that contain the user id fields. We can search for the user id or “USER” and limit the selection to objects types being “MySQL Table” 

Display “All” objects and then select “List of Objects” to select them all. “Visualize” 

MERCHANT_USER_INFORMATION seems to be the table holding the authentication information. 

We can confirm this asumption by looking at the properties of the table MERCHANT_USER_INFORMATION, in the bottom section "Associated to" then property named "Transactions", we can see the list of UI pages that are involved when targetting the MERCHANT_USER_INFORMATION table. Among those transactions, we see several pages touching the authentication features, changepassword.jsp, createcustomer.jsp, logon.jsp, etc. 

 

 

Right-click on “MERCHANT_USER_INFORMATION” and “Add callers” to see which objects are using this Table.  

We can see there are 8 objects, including 3 Hibernate Entities (The types of objects in the view can be identified using the legend). 

 

New functionality to authenticate the user using a cloud authentication service will need to be added. 

The needed changes can be documented using “Document-It” on the view saved and updated 

An action list of objects to investigate/amend can be created using the “Export All Objects And Links” 

 

Select all linked objects and add a TAG to them (name at your convenience). 

This will create a keyword that can be used to find those objects again through the Search feature > Search a tag. 

![Screenshot Recipe Scenario 3](/images/Recipe_Sce3.png) 


Existing functionality that accesses the table will also need to be modified to reflect any changes to the table. This can be seen in the Properties > Transactions section. 