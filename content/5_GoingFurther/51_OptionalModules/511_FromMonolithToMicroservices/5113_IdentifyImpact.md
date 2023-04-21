---
title: "Identify the Impact"
chapter: true
weight: 3
---

# Identify the Impact

## Investigate the user-interfaces and implementation layer 

### User Interface 

Use the right hand side menu to select the object types of the user-interface: _JavaScript Files_ and functions, _JAX RS Operations_. You can easily check how many user interfaces will be impacted: those pages are used to create a booking and visualize the bookings. 

![TicketMonster Booking UI](/images/M2M_13.png)

### Implementation layer 

Select the object type _Java Method_ in the right hand menu to focus the view. 
{{% notice tip %}}
CAST Imaging can highlight within the view the components that are the most complex (cyclomatic complexity) i.e., they are most likely implementing business functions. 
{{% /notice %}}

Select the tag _Complex Object_ in the right hand menu (bottom of the page). This will highlight the most complex methods on the view.

![TicketMonster Booking Java Methods](/images/M2M_14.png)

## Identify components to rewrite  

{{% notice tip %}}
You can highlight the path between the business component and the data source and identify if it does insert/update data into the tables and list the key functions to be rewritten.
{{% /notice %}}

You can start with the Java Method ***createBooking*** that you have just identified as one of the most complex methods of the ***Booking*** table call graph.  

Select all the object types to make them reappear on the view (right hand menu). 

Select the Java Method ***createbooking*** then select the table ***Booking***.  

Finally, right click on ***Booking*** table and select _Highlight_ > _Path_. 

![TicketMonster Booking path view](/images/M2M_15.png)

## Pinpoint the structural flaws 

Before rewriting the business logic in the new microservice, we can identify which improvements could be applied to the new service on its robustness, performance or security. 

CAST Imaging provides an _Insights_ view to immediately highlight components having structural flaws, i.e. critical violations to ***ISO-5055*** best practices. 

Click on the _Insights_ part of the right hand menu and select _Structural Flaws_. 

You can see which components are on the view and having critical violations to ISO-5055 best practices. 

The Java method ***createBooking*** has 2 critical structural flaws impacting performance. 

![TicketMonster Booking structural flaws](/images/M2M_16.png)

## Summary 

**You have now gathered valuable insights on the micro-service candidate dealing with the Booking**:  

- Identification of a data group: the **Booking** and **Ticket** tables have dependency through foreign key, they need to stay together in the microservice database.

- Identification of services using the data group: JAX RS operations 4 GET, 1 POST, 2 DELETE, 1 PUT.

- The Java Method ***createbooking*** holds the logic of the Booking functionality.

- The JAX-RS POST operation ***bookings/***  is the *entry point* of the Booking functionality.

Based on this investigation, a cost vs benefit analysis can be done for final decision making. 

{{% notice tip %}}
 The above process would be repeated for each user-interface and critical implementation method found on the data group call path. CAST Imaging allows to perform the investigation by staying on a single view: the data call graph view of the table.
{{% /notice %}} 

![TicketMonster Booking full view](/images/M2M_17.png) 