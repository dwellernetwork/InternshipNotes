To change settings on a server, we need a Session. You go Properties

We mainly care about Monitoring

SERVICES > DATASOURCE  to go to CCMS.


DATASOURCE is a connection object, gia syndesh stis Vaseis

CCMS Datasource
My main means of communication with the database CCMS

Every server instance (vm) has its own Datasource

We have set the CCMS Datasource to communicate with all servers

With Datasource we have communication with a Database. Without it, we can't.

We must first disable the Target in Targets tab , to stop the server from trying to communicate. Then we cut off the Datasource.

## LOCK EDIT
We must first use Lock and Edit to be able to select any changes in the web logic server
Settings updated successfully does NOT mean its activated yet.
You must click Activate after.
And then you must press:
## RELEASE CONFIGURATION 

To release it from Lock and Edit