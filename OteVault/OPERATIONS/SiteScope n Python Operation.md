What is a SiteScope error ? 
-Errors are written in OBM as well.

How many SiteScopes do we have?
-More than 3. less than a million.
~Sitescope names:
	-Failover


What is our main goal?:
-To see and manage the SiteScope errors 
	~Which categories?:
	-We don't care about Disabled Manually
~To have the errors succesfully present themselves within OBM?
-OBM closes an alarm. SiteScope does not. Alarm still appears in SiteScope.
-The I.T. engineer should not close from OBM. 
	~From Where should he close it ?
		-From SiteScope
-To make an automation 
	~What process do we want to automate?
		-The Query to the db. 
			~We need the query.
			~It needs to be split between different SiteScope categories
				!The idea i have is, I can put them in objects, and ill do a comparison based on the category. 
		-An extraction PER A TIME INTERVAL of the OBS errors
			~We will need the table and its scheme 
		-An extraction from SiteScope Errors 
			~We will need the table and its scheme
			~We will also need the certificates to connect to Oracle
		-The two extractions will perform a comparison
		-There will be a list about which ones exist on SiteScope and not on OBM
		SUM: )
		-The final list output will be in .xlsx


Which database do we connect at to see the errors of sitescope?
-MOM OBM EVENTS

How to see SiteScope Errors?:


How to extract the errors/monitors?:
-Copy all , paste into an excel.
	-This has problems. There's empty or misaligned fields.
~We will look for an API that will give us a JSON or a similar file


Who will we ask for the access:?
-Αγγελική Αναστασοπούλου

What is the current deadline and first step? 
-We must deliver the first sample of the process till next week .On Tuesday.

Known issues?:
-Connection Host Monitor not working
	-Check if the alarm is in OBM, and that its not an error which is part of a current incident.
-Case of connection problems. POAUI. Attempting SSH v2 connect. SSH v2 connect failed
-Depending on the type of the alarm, the appropriate network connections must be made based on Matrix_for_Sitescope.xls
-If the category is "Decommisioned".... //this and one more point on this paragraph. Estimated page: 8 or 9//




RANDOM STREAM OF NOTES ( I'm trying to stay alive!)

-Port 7003 (pvsip01.cosmote.gr - pvsip02.cosmote.gr) - DBServerURS_B2B HA pair(AS_CRM_Support)
-Operations Manager Integration Settings
	-Send Events
-She wants to update the team that this alarm doesnt get sent to OBM because it hasnt been updated to do so. Is this ok? She dont know.
	-THE TEAM MUST KNOW!
-Each time this procedure takes plac,e we ought to create the excels below, mentioning the alarms

