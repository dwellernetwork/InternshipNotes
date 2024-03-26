CFG Module requires refactoring.

 we must verify if CFG has succeded. CFG goes and makes the queries and fetches the data we want from the customers. That's CFG module's work.

error-on-cfg: try, acce

h case - logic for some types of errors. error catching, pop up catching, exceptions etc.

Siebel has some accounts: Those accounts have problems and must be re-submitted. Some customers have a regular account, and a billing account. 
We go to the account, try and access a customer Code

(I must send an IDM Submission to ask for Siebel access)
We go All Accounts in Siebel  > Search > Customer Code. 
We take some pop ups that appear as errors.
Those are the exceptions we catch,
The siebel site resubmits ONLY billing accounts.
We want to be able to resubmit regular accounts as well.


H-case: When we submit a customer, we may have a Popup. We need to handle said Popup. We take the message of the pop up. When we update Vertica (where we throw all the results of each runtime. each runtime has its own identifier)
There is two arrays. Log has something like a runtime registry. When our script ran, when it finished, if it terminated succesfully etc.

We usually need to see the text of the popup to understand the error's nature. 
Alert types: alert on submit (in this case the text appears in the alert and thats where we take our text from. Or there could be no text at all. We need an exception to handle this and tell us there was no submission of the customer).

Those are the most important cases.

Now we are looking at our script to refactor it. We use Selenium. The first thing we want to do is to split it in some modules.

The positive thing is , due to similar automations, the architecture will be similar. On the CFG module we will run some queries, get our registrations.

We will make a customer class.
Then we will have a MAIN module that runs anyhting selenium related.

And then a Vertica module where it has all the functions related to updating Vertica, after runtime is over.
Vertica needs to be updated. First we will need to insert a registration in Vertica to know runtime has begun,
The registration iwll ned a UID. The UID is taken from UID library,
Also, we update Verica AFTER runtime is over .
Customer needs to be updated.
The first insert we did in Vertica , where it says runtime is done, we need to use the UID of that insert to say how our code runtime went.

We take for reference our ready-made script.


### SCRIPT : 

CreateLogFile()
	Creates logs. Uses CurrentDayTime to find day n time
ebmid = uuid.uuid4()
	Makes a UID, Any time we update vertica we use this variable
verticaCon, VerticaCursor = CreateVerticaConnection()
	We make a runtime through this
	To connect to vertica, we need a connection and a Cursor.
	In CreateVertica Connection, we need user: integration to be hashed (itll be left for last)
	It then connects to Vertica and returns the two variables


WriteLog to write logs, Remains the same for refactoring, is custom made

We then run CFG
cfg.ConfigureAccounts()
	it has all the database keys encrypted.
	when we decrypt the codes with the key, we make a connection to the database otemig
	and then otemigmobile and oteFIXED
	We then call GetRefNums
		It runs a query, It returns us our reference numbers that we need
	We close our Fixed connection. we then begin a loop with RunOteMigProcedure. After we took our reference numbers from GetRefNums.
	Goes to oteMic, Runs a query. Its a procedure. It doesnt do anything else.

Reference Numbers are orders.
otemigCon.close() 
then we are done with that


We write a log. We go back to otemig. key, fer, enc0... till decsoapDB needs all to be refactored, it does not belong there. A new module for SOAP.
We open two databases ,We make connections for them both. We make a connection for OteMig.

If there is an error when we try to connect to OteMig, we must make a reconnection error. It is rare but there needs to be an exception.

When we connect to OteMig, we go and connect to the soapDb. We have two connections now.

customerIds, orderIds, customerCodes, customerBarids.......custIntergList all needs refactoring. 
We will make a customer.class that will do all this instead. Less payload in the functions.

We got some lists, we fill them from GetCustomerCodesFrom DB (uses OteMigCursor,SoapDb,OteMigCon)
	It has some empty lists. We get customerList and fill it from OteMig. OteMigSomething runs a query. the query gets the info. Takes all the rows it found and puts it in results (theres a row loop for this at the end)

def GetInfoFromOTEMIG(cursor):

Number of codes received from OTEMIG:
	we then do GetCustINteg(customerList)
	we get the 4th (n-1  = 3rd registration if we start from 0), OTEC2610411 in this case.
CheckIfCustomerExistsInSEQ

We run a simple query. We ask it "see if Cust_Integ is in the database", and the operation is CreateCustomer.

We then to the list of the ppl that exists inside the sequencer ( #whatisasequencer)

def GetCustomerCodesFromCustomerList creates some lists and puts through stuff from customer[] array. It will all be refactored into customer class 


We now have all those customerIDs, orderIDs, customerCodes lists. 
We then got som eWriteLog(CurrentDateTime()

We can see logs for errors.

If len(customerList) > 0 :  checks if there is even one customer. If not, it stops
If it does, we go to the loop and it submits all the information we got. It returns a list with all the status, failed, error, and successCodes. 

We go to the SubmitCode. This one is a Goliath.
	driver = GoToSearchAccount() (this is a robot that goes n find stuff)
		firefox_options= is because it works with firefox. --headless means it does not need to open the window. FOR DEBUGGING WE DEACTIVATE THIS
		wait = WebDriverWait (this is a custom wait)
		Robot goes and opens a website. //it does not log into the balancer. It logs via Oracle
		After page is opened, we search for an element with a username. 
		Our driver comes to a page. Then we tell our robot "go and find an element type = input, and name property = this shit"
		If we do an inspect on the User Id field of Oracle, it has those exact properties. It goes and submit.
		THeres a lot of time.sleep . Not a good practice to use, but in Siebel it takes time to load all the elements and their ids change in the first initialization moments.
		It sleeps till it finds the elements with a particular id.
		Anyway it goes and submits the username after it finds the field.
		element type = a is for linux. 
		all this code is to log in siebel
		After it logs in, shit, what is element = driver.find_element. 
		element.click to click the element. its in all accounts now.
		now we search using customer ID. If we do an inspect : id = 14_0_ctrl
		Our driver returns back to submit through this.
		We then return our driver from the go_search account. We make some emtpy lists. We put in some status for each customer. And now, we do a loop for each customer. We make a log, and then we run the function TestSubmit. 
			Goes in Selenium and runs for the customers info
		It then returns if it was successful n an errorCode in case of errors
		Element tabScreen finds 
	Test submit goes back to accounts. Goes to allaccounts, n we click on Search. We look for input element that says "ote customer code"
	after we select this, we go to TestSubmit. It has the customerCode
	Customer request Administration
	Go to view not enabled (update se pending)
	element.is_enabled():
	If not enabled we cant click it. We need to write a log, and go back to accounts, and do an update to OteMig that for this customer, we couldn't go to view this customer.
	If gotoview IS enabled....aaaand we brought out a customer example and i got lost a bit.
	submit button not enabled etc etc.
	if element.is_enabled, we try to click it. we wait a bit, and then we check if submit is done properly or not. wait.until.element is a better idea than time.sleep . In dynamic pages , the element will change ID. Time.sleep(0.1) is a better idea as well
	-
	-Get popup text. It may fail to do so. Thats why try except is the way to do this.
	 IF POPUP APPEARS, Go and get the text . EXCEPTION IN THIS CASE, IF IT GETS CAUGHT, MEANS POP UP HAS APPEARED.
	updateIOteMigWithError throws our popup text for the error.
	-
	-When we are done with all the customers and the pop ups etc etc we close the Driver. It submits a log that says if things went well or not.
	-if len(customerList) != len(statusCodes):
		do an update to vertica that procedure went unsuccsessfuly
	-else:
			OtemigConn.close()
			soapDbconn.close()
			vertica (we open connection)
			insertVertica_OT_Automation_Log_Detail
			after we submit all customer info at vertica, we UPDATE vertica
			we tell it the procedure went fine.
	There is an except that things just didn't work out with the procedure.
			
	
		





***Lydia says:***

We have some order cases. Customer wants to buy a double play for example. he was an existing customer with other assets. But the entity of Customer hasnt been created properly. We have the Customer Lydia. Lydia has some billing accounts. 3 different accounts, one for her mom, one for herself, and a second house.

We got the amount of products . Lets say we want a new OTE TV . It goes through an order through Siebel. It falls upon OSM to do the Order orchestration. The order has to go through many systems to perform this process. OSM is the middle man in all this.

OSM first checks on the Customer entity and the account. When  we fetch the Reference Numbers, we are fetching the Orders via OSM. Our goal is to fix the customer entity.  


