---
title: "Application Discovery"
chapter: true
weight: 3
---

# Application Discovery 

**Objective** : Before you begin the modernization process, you must first understand the as-is architecture of the system and understand : Which are the technologies being used ? How do they interact ? Are there isolated layers which code is not referenced ? What are the frameworks in place and are they compatible with the target platform ? etc. 

## Understanding the technologies and size 

Select the application named ***Demo_Express***.
Information on the application size, number of lines of code, number of objects, etc. are displayed along with several navigation scenarios.

Choose the scenario *Explore the interdependencies* > *Between technology objects* to explore the objects composing this application grouped by technology types.
![Welcome](/images/DemoExpress_welcome.png)


## Understanding the architecture 

You are now positionned at at the Level 5 of the navigation perspective.

You see that ***Demo_Express*** application is composed of Cobol and Java which can raise up a few questions : 
- What are the communication mechanisms between Cobol and Java ?
- What is the role of the Cobol layer ?
- How is the DB2 database consumed ?

To answer those questions, you would need to explore the architecture in more details down to reading the source code.


![Screenshot DemoExpress Level 5](/images/DemoExpress_Level5.PNG) 

:memo: By exploring the view, you can identify the below characteristics of ***DemoExpress*** application that will be useful for the rest of the journey : 
- a Presentation Layer with JavaScript and HTML, JSP Pages 
- the implementation layer contains Struts and Java
- you can see that Apache Log4j is used as logging framework  
- the DB2 database is accessed only by the Cobol Programs mostly through DB2 Views (280 References from Cobol Programs to DB2 Views versus 10 References from Cobol Programs to DB2 Tables)

You will now investigate the 34 references between Java and Cobol.

Double click on the edge between the Java Classes and the Cobol Programs, you can change the Graph Layout to *Sequential* to have a better display.
![Screenshot DemoExpress Level 5](/images/DemoExpress_JavaCobolall.png)
You can see that for one Cobol Program, there is one Java Method calling it, the parent Java Class is also represented with a dotted line towards the Cobol Program, representing the escalated reference with the Cobol Program :
![Screenshot DemoExpress Level 5](/images/DemoExpress_JavaCobol.png)
 
You can now right click on the edge between one Java Method and one Cobol Program and *Show the source code* to identify which mechanism is used is this link and you can see that this is very similar to JDBC calls : 
	
	public void execute(IDbRequest dbRequest, IDbResponse dbResponse) 
	throws DBException, SQLException {
		SPName = "COBOL_PROGRAM_NAME";
		...
		cstmt = con.prepareCall("{ call " + QUAL + "COBOL_PROGRAM_NAME(?,?,?,?,?,?,?) }");
		...				
		rs = cstmt.executeQuery();
		...
	}
	
:memo: In the application ***Demo_Express***, the Cobol Program operates as a Stored Procedure to execute the database calls sent by the Java layer.


### Application Recipe

Now select the application named ***Recipe*** and apply the same navigation steps than above.
 ![Screenshot Recipe Level 5](/images/Recipe_Level5.png)

You understand rapidly the high level characteristics of ***Recipe*** application :
- Presentation Layer with Active Server Pages, JavaScript and HTML
- Logic Layer in C# Classes
- Data Layer with C# Class DAO with SQL Server Procedures, Tables, Views and Functions
- Among the APIs used in the application, we see .NET System Diagnostics Logging framework
- The SQL Server tables are accessed by C# but also by SQL Server Procedures, which is not a recommended architecture design to ensure database integrity. 

But are those SQL Server Procedures really used by the C# layer ?
Right click on the node *SQL Server Procedures* > *Children+caller/callee* to identify the adherence with the C# Classes.
![Screenshot Recipe Level 5](/images/Recipe_SQLProc.png)
 
Now hide the type *SQL Server Tables* in the right hand legend : only a few SQL Server Procedures show no references to neither SQL Server Functions nor C# Classes. 

:memo: This confirms that the SQL Server Procedures are really referenced by the C# layer, the code they contain needs to be maintained.

![Screenshot Recipe Level 5](/images/Recipe_SQLProcDetails.png)


**You now have, in a few clicks, gathered valuable insights on the applications to move on to the next step of the journey and study several modernization scenarios.**

Close the view to get back to the Level 5 perspective and prepare for the next exercise.

![Screenshot Recipe Level 5](/images/Recipe_closeview.png)