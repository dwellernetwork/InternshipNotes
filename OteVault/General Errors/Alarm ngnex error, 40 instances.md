Error while processing the execution os slob wnga eligibility. Connection has already been closed . 

Potential error source: Datasource

**MAIN ISSUE:** "Eligibility of Prometheus" is our issue. It is occuring on ALL servers.
Αναπτυξη and Provisioning must be updated via email. We send the error request. The first "τριαρι". "Failed connection error"


How do we find the Datasource?
JMDI (or jadi i didnt hear well) 


WE are looking for NGA_ELIGIBILITY.wsdl (from the oracle web server)
Pipline, Proxy, Biz
We are interested in DBStoredProcedureInteractionSpec
Globe = σχημα. shape name. 


You open Biz
Datasource is inside the biz.
Then you go to References. You click the orange symbol thing on th eright wayyy to the side of the screen,

There is a bunch of code there.
You find a line inside eligibility. Thats the datasource.

globe.procedure.nga.elibigility

The procedure what we are interested in.




'Καλωντας τη procedure NGA_ELIGIBILITY στο σχημα GLOB λαμβανουμε το παρακατω error:
(the error is too big to copy with my hands)'(unable to convert the SXD element P_OUT_NEw_PARAM_NGA whose JDBC type is ARRAy to a corresponding XML document java sql.SQL.exception no data found ORA-01403 no data found )RA-06412: at line 1 ) (this is the most I could copy by hand)

Service Provisioning & NI is where this error was sentT

The issue does not change any information on Dynatrace sadly. Cannot trace it there (at least we have not set up the right monitoring tools to do so)



Random Error Case
	OTE_EXA_CUST_LOGGING
	
	It belongs to  SDP department. You call there