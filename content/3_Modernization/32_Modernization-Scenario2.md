---
title: "New Authentication Layer"
chapter: true
weight: 2
---

# Replace a custom authentication layer

**Objective**:  the application ***eCommerce*** uses a custom authentication mechanism which we would like to replace with an authentication service such as AWS Identity and Access Management. 

But what are the source code components involved and what are the impacts of this replacement ?

**Documentation**:  This exercise will utilize the CAST Imaging *[Transactions](https://doc.castsoftware.com/display/IMAGING/User+Guide+-+Transaction+scope)* and *[Data Call Graph](https://doc.castsoftware.com/display/IMAGING/User+Guide+-+Data+Call+Graph+scope)* features. 

## Identify components to be replaced 

Select the application ***eCommerce*** at Level 5 perspective (from the Welcome Page, choose *Explore the interdependencies* > *Between technology objects*). 

This application is composed of a UI layer in JSP and Javascript, Struts and Hibernate are also in use with a MySQL database.

You can start by identifying the components involved in the Login phase.
Change the scope from *Application* to *Transaction* and search for the transaction named ***logon.jsp***.
![Screenshot Recipe Scenario 2](/images/eCommerce_transactions.png) 

:memo: You now see all components types involved when executing the logon.jsp page which involves calls to the MySQL Table.

On the left hand menu next to *Levels*, click on *Objects* to display the individual components involved in the logon.jsp transaction.
![Screenshot eCommerce search](/images/eCommerce_transactionobj.png)

The full list of components is quite heavy, but the right hand side menu helps you filter the object types visible on the view. 
Display only the MySQL tables of the view and identify the table which are holding the User information.
![Screenshot eCommerce search](/images/eCommerce_logonjsp.png)

Vizualize the source code of the table named MERCHANT_USER_INFORMATION, you can see columns related to ADMIN_NAME and ADMIN_PASS. 
![Screenshot eCommerce search](/images/eCommerce_logonjspsrc.png)

You can also verify the properties of the table MERCHANT_USER_INFORMATION: select the table and display the *Properties* section on the right-hand panel (next to *Objects*). Scroll down to the part *Associated to* then select the property named *Transactions*. 

You can check out the list of other transactions where MERCHANT_USER_INFORMATION table is involved, they are identified by the name of the UI Page which starts the transaction.

Among those transactions, several pages concern the authentication features: *changepassword.jsp*, *createcustomer.jsp*, etc. 

![Screenshot eCommerce search](/images/eCommerce_properties.png) 

Now, still in the *Properties* section. Move down to the part just below named *Data Call GRaph(s)* and choose "MERCHANT_USER_INFORMATION" in the list. 
![Screenshot eCommerce search](/images/eCommerce_properties_data.png)

Those are all components involved with the table MERCHANT_USER_INFORMATION, meaning all components which are calling the table + all their callers.

![Screenshot Recipe Scenario 2](/images/eCommerce_datacallgraph.png)

## Document the changes to be made

We have seen in the previous workshop how to Save, Document and Export a view in CAST Imaging.

{{% notice tip %}}
Another way to save your work is to attach a *tag* to the nodes of interest. The *tag* is a keyword which can be used to find nodes through the *Search* feature > *Search a tag*. *Tags* are shared within all CAST Imaging users of the same application and appear in the properties of the node.
Learn more on the *[Tags](https://doc.castsoftware.com/display/IMAGING/User+Guide+-+Working+with+tags)*.
{{% /notice %}}

Locate the table MERCHANT_USER_INFORMATION on the Data Call Graph view by using the *Object Search* button.

![Screenshot Recipe Scenario 2](/images/eCommerce_objsearch.png)

Select the nodes linked with MERCHANT_USER_INFORMATION: there are 3 Hibernate Entities and 5 MySQL Unique Constraints.
Select also the Java Class named *MerchantUserInformation* which is linked with the Hibernate Entities.
Add a *tag* to the selected nodes that you can name freely. 

![Screenshot Recipe Scenario 2](/images/CreateTag.png) 
![Screenshot Recipe Scenario 2](/images/eCommerce_tag.png) 

You can now retrieve the nodes that have been tagged through the Search feature.

![Screenshot Recipe Scenario 2](/images/eCommerce_Search.png)
![Screenshot Recipe Scenario 2](/images/eCommerce_searchtag.png)
 
:memo: The data contained in *MERCHANT_USER_INFORMATION* should be ported to the new authentication layer, and the components directly calling the table should eventually refer to the new authentication service API.
*Tags* in CAST Imaging allow to retrieve those objects in one click.


## Identify the impacts 

**You now know that the whole call path to the *MERCHANT_USER_INFORMATION* table will need to be retested.**
**The *Data Call Graph* feature in CAST Imaging precisely displays all objects up to the UI layer that are involved with this table.**