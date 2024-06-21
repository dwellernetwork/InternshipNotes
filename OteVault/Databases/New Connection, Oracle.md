Click the + Green sign for a new connection

Example of an address link to connect to a db:

NGA@//omdbd-scan.ote.gr:1521/OTECUST

and

EAIBUSPROD6@//172.18.28.59:1523/BUSDB


-The first part (EAIBUSPROD6  or NGA) is the user session (kinda the name of the database). 

-Next is the IP. It does not have to be numerical. omdbd-scan.ote.gr is an IP for example

-Then the port number

-Finally, OTECUST as well as BUSDB is the SID or the service name. It is one of the two. We use Test to see if we connect to the one, and if not, we try the other

-Now we will also need from Keeper the password for this specific database. We go looking using the user session/db name, and follow the verification process.

-We click "save password" to retain the connection. We always first use Test, not Connect. Connect comes after. 


## DOMAINS
We have 123 domains currently in WebLogic
## WHAT IS DATASOURCE




