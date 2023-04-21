---
title: "Discover the architecture"
chapter: true
weight: 1
---

# Discover the architecture 

**Objective**: With the goal to transform the monolithic application ***Ticket Monster*** to micro-services, we need first discover the architecture of the application to understand the technologies involved and adherences between the application layers, specifically the data layer which will be the starting point to determine a micro-service candidate. 

## The Ticket Monster application 

Select the application ***Ticket Monster*** and investigate the application at the _Level 5_ perspective: 

![TicketMonster_intro](/images/M2M_4.png) 

***Ticket Monster*** is a monolithic Java/Web/MySQL application (the node name for MySQL is _ANSI Table_) with a JAX-RS API. The data layer is composed of 12 tables, accessed only through 12 JPA Entities.  

Double-click on the link between **JPA Entity** and **ANSI Table** to visualize the links between those nodes.  

You see that the data access is properly designed with a single JPA Entity attached to a single table. 

![TicketMonster - links between JPA entities and Tables](/images/M2M_5.png) 

![TicketMonster - one to one link between JPA and Tables](/images/M2M_6.png) 

## The decoupling journey starts 

Let's start the by choosing the best micro-service candidate for the iteration. We need to identify the adherences between the data sources based on foreign keys. 

Click on the node **ANSI Table** to visualize all tables and their dependencies.  

![TicketMonster - Adherence between tables](/images/M2M_7.png) 

You can observe that tables are quite dependent on each other, so we will have to categorize the **data groups**, that is _tables that will need to be together_ in the target microservice database. 

Now, we have to identify the relations between data sources and transactions to better understand the adherence to the implementation layer and the tables utilization.