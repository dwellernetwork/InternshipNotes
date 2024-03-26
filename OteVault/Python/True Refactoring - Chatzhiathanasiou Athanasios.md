Our files are:

verticaModule.py
customer.py
retrieveOrders.py
submitCustomerProcedure.py
main.py
retrieveCustomer.py


Στο αρχειο:  
### retrieveOrders.py

Εχουμε:

def ConnectToOsmFixed():    (συνδεεται στη βαση σταθερης OSMFIXED)
	pass
def ConnectToOsmMobile():  (συνδεεται στη βαση κινητης OSMMOBILE)
	pass


def RunProcedure()
	pass
def RetrieveOrders
	cursor : ενα ρομποτακι στο connection που κανει queries που ζηταμε (με ποντικι)
	δεχεται το key με το οποιο κανει decrypt τον κωδικο 
	εκτυπωνει το αποτελεσμα
	συνδέεται στη βάση σταθερης και κινητης OSM
	λαμβάνει τα reference numbers που αντιστοιχουν στα orders
def GetMobileRefNums(cursor):
	κανει fetch μέσω cursor και query  το reference number της βασης mobile. κάνει ένα λουπακι και αποθηκευει τις μεταβλητές σε πίνακα.
	το cursor είναι ενα ρομποτακι που κανει κλικ για εμας και τρεχει queries

def RunProcedures(refNums,cursor, con):
	query=f"


ΣΤΟ ΑΡΧΕΙΟ 
### Customer.py

def __init__ (self, rowId, orderId, customerCode, custInteg, baRowId, baCode,action):
	self.rowId = rowId
	self.orderId = orderID
and so on and so fotrth.

printCustomer

GetCustomerStr

make_customer



ΣΤΟ ΑΡΧΕΙΟ
### retrieveCustomers.py

def ConnectToOtemig(password):
def GetCustomerData

def RetrieveCustomers():
	has key. decrypts pass, prints decrypted key. 
	-connects to Otemig
	-otemigCursor.otemimg
	- encryption is problematic. it wants binary. we use directly the pass cauz we had issues with the variable 
soapCursor.soapCon = ConnectToSoap (decSoap) 
κανει return απο τη ConnectToSoap το soapcursor και το soapCon

checkifcustomerxistsinbussequencer(customer, cursor):
	query=f""
	cursor.execute(query)


### verticaModule.py


def InsertIntoLog

def InsertIntoDetails ( cursor, con, ebmid, orders, duration comment)  
	Has a query
	cursor.execute(query)
	exit()

def UpdateLog

def CreateEbmid
	
def ConnectIntoVertica
connects into vertica and logs in with a password

def EncryptPass():
	has a pass that we encrypt with the key hash
	we turn the key into bytes
	we use decVertica to decrypt the key afterwards




## MAIN PY

FinalizeVertica : the final update to Vertica
InitializeVertica: It connects to Vertica.. uses ebmid =verticaModule.createEbmid
ebmid is sent when we Finalize


RUNTIME
------------------
When it finds a popup, it accepts and continues after it stores the text.
