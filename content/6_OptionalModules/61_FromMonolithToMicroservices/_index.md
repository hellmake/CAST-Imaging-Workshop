---
title: "Monolith to microservices"
chapter: true
weight: 1
---

# From monolith to microservices 

## Why Refactor to Microservices? 

![Why refactor to microservices](/images/M2M_1.png) 

## Scope of this module 

In this module, you will investigate an application that has already been scanned on CAST Imaging, learning how CAST Imaging supports the incremental transformation flow based on the Strangler Fig Pattern:   

![Incremental Flow](/images/M2M_2.png) 

 ## Strangler fig pattern 

The best approach for decoupling a monolith is to proceed incrementally: one microservice should be designed, developed, tested, and deployed in production before proceeding to the next, which helps to continuously learn from each cycle. 

During the transformation, both the new application and the monolith co-exist in production. Over time, the amount of functionality that is implemented by the monolithic application shrinks, the gradual replacement being transparent to the end-user. 

Technically speaking, decoupling functionalities from a monolith requires careful isolation of the data, logic, and user-facing components and their redirection to the new service. To prioritize the best candidates for a decoupling iteration, key criteria need to be evaluated: 

1. Level of dependency: from a clear view of the dependency types (data or services) and the level of impact between modules, we identify the _loosely coupled modules_ which are the best candidates to start the iteration.
2. Data integrity and synchronization: functions and their related data should be split together, based on the service boundaries, to avoid reading data from and writing data to multiple databases even temporarily.
3. Business criticality, evaluation of cost versus benefits, comprehensive test coverage, application security posture, organizational buy-in. 

**CAST Imaging helps understand the natural boundaries that provide the right level of isolation for each micro service, and iterate until the best cost/benefit ratio is reached:** 

## Monolith analysis and microservices determination in CAST Imaging 

![Detailed approach](/images/M2M_3.png)