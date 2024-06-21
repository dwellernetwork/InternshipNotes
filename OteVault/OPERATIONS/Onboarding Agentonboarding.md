
I need to find what services DataPower calls . The systems are X or Bus.  What services are calling Datapower in this case? Are we looking for the services calling other services on DataPower? 


ONGOING INVESTIGATION:
--
--INTELLI
	-Inspected DataPower in dynatrace. No intelli in the processes.
	-Searched for Intelli in Dynatrace. No results
	-Searched Synchordia for communication with DataPower in Dynatrace. No results.
	 -Learned from Integration and Portals its general function, and that its within an Azure cloud.


--Services: DATAPOWER_ACCESS_LOGS
	-CosmoteApplicatioNServer:443,8590
		-

QUESTIONS:
----------
WHAT IS INTELLI?
ANSWER: Intelli is a service that handles the signing of documents. It runs on Azure Cloud. It also has two synchordia services running, but they do not communicate directly with each other. 

how did we find Docker,  osb sync and data power communicate with the app server? (discerning process names)
ANSWER: -We find them via DynaTrace, when we go to a host> our web server name. There, we see processes that are calling the server, and processes BEING called by the server.
how do we find the ports?
ANSWER?: ~Most likely through query...
Is the OSB sync cluster correct?'
ANSWER!:-The OSB sync cluster is a cluster of 3 node.s


195.167.99.3  + 195.167.99.4  load balancer 

CHANGES TO BE DONE
-7075, 7076 are two ports that will go together on onboarding. 
The rest of the ports, (all the 8186, 8085, 8086) each will come separately from elsewhere .Each with its own color, same for the services.
-Delete connection to the databases for now. Leave them inside
-Stretch the Web server box, make it larger. Put the monitors in each of the two boxes spread apart a bit, and throw the server names with their respective ports in-between
-Remove all reference of port 80.
-Color code the sites in accordance to their ports. 7075, and 7076 will be colored blue
-Remove connection to the cloud for now. Move datapower at an accessible place away from all entities.

-Create connetions to DataPower and OSBSync on pvwebdahr03 and its dr server.
-Create connections to Datapower, OSBSync, Docker +Kubernetes, and a Siebel Load Balancer + Siebel from the app servers.

[1:32 μ.μ.] Sabati Stavrina

eixame dei xthes alla den to thimamai

[1:34 μ.μ.] Sabati Stavrina

to oracle service bus prepei na leei OSB sync mesa epipleon giati texnologia oracle service bus exoume kialla

[1:39 μ.μ.] Sabati Stavrina

kai to siebel LB eixame dei oti kapoio sigkekrimeno service stelnei pros afton ton server alla den thimamia poion server enw esi exeis valei oti o application server milaei me ton LB opote thelei ksana anoigma

[1:50 μ.μ.] Sabati Stavrina

kai nomizw exeis ena tipografiko sto onoma tou server pvappbrddr01

[1:50 μ.μ.] Sabati Stavrina

o enas application server einai aftos edw


-Build the web and app servers EXACTLY as Lefteris has. Even the spacing.

Answers:
-----------

MY INBOUND URIS FROM DATAPOWER:
|   |
|---|
|/ProductCatalogue/api/configurator|
|/SYNC/INBOUND/DOB|
|/SYNC/INBOUND/DOB/BypassSynchordiaVerification/2-41W2BOXN|
|/SYNC/INBOUND/DOB/CompareImages|
|/SYNC/INBOUND/DOB/GetAllSignedDocuments|
|/SYNC/INBOUND/DOB/GetBatchHistoriesByBatchId|
|/SYNC/INBOUND/DOB/GetBatchHistoryByBatchId|
|/SYNC/INBOUND/DOB/GetBatchHistoryItemFields|
|/SYNC/INBOUND/DOB/GetBatchHistoryItems|
|/SYNC/INBOUND/DOB/GetBatchHistoryItemsFromBatchHistoryId|
|/SYNC/INBOUND/DOB/GetBatchWithMetaBySRID|
|/SYNC/INBOUND/DOB/NEO/RegisterRequest|
|/SYNC/INBOUND/DOB/NEO/StartProcess|
|/SYNC/INBOUND/DOB/RegisterRequest|
|/SYNC/INBOUND/DOB/StartProcess|
|/SYNC/INBOUND/OneApp/DOBNeo/GetRequestStatus|
|/SYNC/INBOUND/OneApp/DOBNeo/RegisterRequest|
|/SYNC/INBOUND/VPOS/PaymentGateway/581667895131198000000219340082/payment|
|/SYNC/OUTBOUND/DOB/StartProcess|


MY PORTS:
|   |
|---|
|577|
|449|
|455|
|4444|

MY OUTBOUNDS:




Panagiota Karamitsou's Diagram:
	
	siebel sends to pve (pr.ote.gr) . pve communicates with application server with sftp protocol. This is a file system.
	
	Siebel does a PUT sftp to pve. We do a klisi to siebel and thats how it pulls them, our klisi doesnt go through pve. but when it sends, as an answer to our call, it DOES go through pve.
	
	When we get them, we put them to a Cif. the cif has the ip 10.101.6.9. This will need to be presented, its going to be a full duplex communication (file put)
	
	Our app server in this example is pvappbrddr01 and pvappbrdah
-----------------------------------------

External Load Balancer (onboarding.cosmote.gr) and Intrenal Load Balancer (agentonboarding.cosmote.gr):
	Intelli Azure Cloud: Synchordia and Signature.
	
	
	
	
	
OUR DATABASE IPs:

	pvsqlbrddr02.ote.gr 10.53.42.121
	pvsqlbrdahr02.ote.gr 10.53.42.121




WHAT MORE TO ADD:

>REMOVE ONBOARDING AND AGENT PORTALS
>REPLACE THEM WITH WEB SERVER ON THE WEB SERVERS, AND APP SERVER ON THE APP SERVERS
  FIX THE ARROW, IT GOES FROM WEB SERVERS TO APP SERVERS, NOT FROM LBS TO APP SERVERS
  PUT THE PORTS ABOVE THE BOXES, FROM LB TO WEB SERVERS
  SAME WITH APPS, PUT THE BORTS ABOVE THE BOXES, FROM WEB SERVERS TO APPS
  TAKE THE IIS ICON MONITOR



BASIC QUESTIONS:
	Which are the servers I care about?:

WHICH SERVERS ARE ON DYNATRACE:
-----------------------------------------------------------------------
	WEB SERVERS
	pvwebrddr01 IS
	pvwebrdahr03 IS
	
	pvwebrdahr02 IS
	pvwebrddr02 IS

	APP SERVERS
	pvappbrddr01 IS (and its the same app server for both onboarding and agent onboarding)
	pvappbrdahr02 IS (and its the same app server again)
	

FOR ONBOARDING:
	MY WEB SERVERS:
		>pvwebrddr01: 10.53.217.60
			>CosmoteDOBSignalIR (.8186 http)
			>CosmoteDOBWebApiPortal (.8085 http)
			>CosmoteNOE (.8086 http)
			>CosmoteWEBPORTAL (.7075 http, 7076 .http)
			>Default Web Site (.80 http)
		>pvwebrdahr03 10.53.147.47(7075,7075 port for both)
			>CosmoteDOBSignalIR (.8186 http)
			>CosmoteDOBWebApiPortal (.8085 http)
			>CosmoteNOE (.8086 http)
			>CosmoteWEBPORTAL (.7075 http, 7076 .http)
			>Default Web Site (.80 http)
			>--------THEY ARE THE SAME SITES--------<
	MY APP SERVERS:
		>pvappbrddr01 10.53.202.221
			>Cosmote_Proxy(.9095)
			>CosmoteApplicationServer (.8590, .443 )
			>DashBoard (.8690)
			>Default Web Site (.80)
		>pvappbrdahr02 10.53.131.240 (8590 port for both)
			>Cosmote_Proxy(.9095)
			>CosmoteApplicationServer (.8590, .443 )
			>DashBoard (.8690)
			>Default Web Site (.80)
FOR AGENT PORTAL:
	MY WEB SERVERS:
		pvwebrdahr02: 10.53.156.50 (443)   (t1-prod-groupnet gr) (remote machine: name of machine.groupnet.gr. Thats how you log into them via cyberark. In this case, pvwebrdahr02.groupnet.gr)
			>AgentPortal (.9095, .443)
			>Default Web Site (.80)
		pvwebrddr02(same as above to connect to this) 10.53.217.35 (443, 9095)
			>AgentPortal (.9095, .443)
			>Default Web Site (.80)
	MY APP SERVERS:
		pvappbrddr01 10.53.202.221 (9095)
			>Cosmote_Proxy (.9095)
			>CosmoteApplicaitonServer (8590, 445)
			>Dashboard(8690)
			>Default Web Site (.80)
		pvappbrdahr02 10.53.131.240 (8590)
			>Cosmote_Proxy (.9095)
			>CosmoteApplicationServer (8590, 445)
			>Dashboard(8690)
			>Default Web Site (.80)


10.53.42.123 pvsqlbrdls









MY LOAD BALANCER IPs
--------------------------------------------

Server:  dnscache02.cosmote.gr
Address:  10.53.62.240

Name:    onboarding.cosmote.gr
Address:  195.167.99.46  <--------- load balancer n1


C:\Users\gmpoulas>nslookup agentonboarding.cosmote.gr
Server:  dnscache02.cosmote.gr
Address:  10.53.62.240

Name:    agentonboarding.cosmote.gr
Address:  10.53.162.54  <----------- load balancer n2 


They are all windows servers

10.53.162.234:
-------------------------
port 8186 ( 7075 , 7076)
You go to site bindings:
(It has http, not https in this case)

cosmoteDEO, 8186, 8085, 8086, 7075


ΕΙΔΑΜΕ ΤΟΝ DR 01 , και το NAHR 02

![[Pasted image 20240603165010.png]]

AGENT ONBOARDING PENDING TO BE SEEN (DR 01 , και το NAHR 02 τα αντιστοιχα του onboarding)