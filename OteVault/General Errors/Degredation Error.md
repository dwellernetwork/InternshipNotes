Instance 1:


ISSUE: The server has double/triple the processing time per request than usual (Usual peaks at 1s. Things went to 2-3seconds and sometimes, beyond)
OSB Recharge (web server)

-First move we do: We search the error in the database.
-We look at the request and we see what function it performs.
-We check the server's health and status, by logging in the WebLogic server platform.
	-In this instance, the server's health seems good.
-We attempted pipelining the error (viewing it through the Message Flow). 
	-We entered the final , bottom node of the tree. This lead to another tree
	-Results on the final node of the next tree: inconclusive
-We then connected to the linux terminal of the server to observe the logs

GENERAL RESULTS: INCONCLUSIVE
The issue fixed itself



