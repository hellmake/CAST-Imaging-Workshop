---
title: "Exploring the Results"
chapter: true
weight: 3
---

# Exploring the Results

After doing the work of
- registering applications,
- scanning them,
- uploading their scans results,
- and enriching those results with survey answers,

we can now move on to the exploration of the insight gathered for those applications.

{{% notice info %}}
This workshop follows a bottom-up approach, which means that we'll first explore the individual results for the applications we just scan and later on we'll see how they are consolidated into the whole portfolio. Following this workflow, you'll see a lot of information about the other apps and the whole portfolio. Worry not - we'll get to that in the next chapter.
{{% /notice %}}

## Chapter Overview

This chapter will perform a deep dive into our two applications on the following aspects:
- **Cloud Readiness**: how fit are those applications for being deployed onto a PaaS? And what can we do to improve that prospect?
- **Software Composition**: what are the risks posed by the third-party libraries leveraged by our apps?
- **Software Health**: how good is the app's code itself? Is it sturdy, clear and maintainable?

All these aspects are fundamental to drive a move-to-cloud or modernization project, and we'll later see how each can impact the project.

## Where to find our new apps

Let's find our way back to the main *landing page* by clicking on ***HOME*** in the top menu. Now let's scroll down on that page until we see the list of ***Latest Onboarded Apps***:
![Latest Apps](/images/DetailedIntro-1.png)

{{% notice info %}}
If at this point you can't see the apps in the list, it could be that you've been faster than CAST Highlight. Once an application's result are submitted, the web app takes a few minutes to recalculate all of the portfolio's demographics. Grab a cup of coffee before refreshing the page.
{{% /notice %}}

Click on the name of *jAlbum* and you'll be taken to

## The Application's Dashboard
![App Dashboard](/images/DetailedIntro-2.png)
This is the indivual page for this application. From here, we'll be able to access all the data extracted from it. Without going too much into each item, you can already see the following info (most KPIs are rated from 0 to 100):
- ***Software Health***, which is the average of 
	- ***Software Resiliency*** (how **sturdy** the application is)
	- ***Software Agility*** (how **maintainable** the application is)
	- ***Software Elegance*** (how **non-complex** the application is)
- ***Cloud Readiness*** (how ready the app is for being hosted on a **PaaS**)
- ***Open-Source Safety*** (how safe safe are the 3rd-party libraries used)
- ***Business Impact*** (how important that application is for the company. This is derived from the answers to the *Business Impact* survey you filled out a few minutes ago).

Below the application's name, you can see the application's menu (we're currently on the ***Overview*** tab), which is where we'll navigate through the various screens detailing the insight gathered about the app.

### Onto Cloud Readiness
Click on the ***CloudReady*** tab of the application's menu, and we'll see if it's ready to fly...  