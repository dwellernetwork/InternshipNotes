Deployment:
Code upload. Change, addition or removal of code from an application. 
Can also be just a config file. It comes from application support.
Even a certificate is a deployment.


Patch:
Change of software of the machine specifically. If there is a security change or changes on the kernel. Its changes on the host essentially. SECURITY REASONS are the most significant reasons.
Oftentimes there needs to be a reboot for the patch .
Usually has to do with Linux admins or Windows admins.
There are some 'prepatch' actions  that are usually performed by Application Support. We make sure that anything that runs on the machine that has to cease function for the patch to occur. We go through them to reduce the "impact".
Example: When you patch a server where OSB is running, prepatch actions are calling the network admin, and asking them to remove the network from the balancer.

Release:
All major deployments happen at the same time at a time of availability of service
- Aftercare, one week post Release.
- There is a vendor writing this code sometimes. For example OSB
- Cognity writes the code for that. They maintain the code for OSB
- Whenever there is a problem that needs to be changed, we submit to PBI.
- PBI is a ticket system, it goes to Development
- Development gives you a date of ylopoihsh
- Then it offers to you so you can deploy it, after it is tested.
- This has a cost, there needs to be research done and code to be made
- The company has the responsibility to fix the code for this one aftercare week, For Free.
- BUT, IF we are late and we dont find the issues on the first week, its like a New PBI ticket. Costly in terms of both money AND time.


Πατσιερα: You can observe the actions of the patch happening.

Post-patch actions: Restarting machines.


THERE IS PATCH IN APPLICATION as well
-Sometimes we may patch something like Coherence from Oracle
	(Coherence upcoming patch is a good example)
-Its also called "upgrade"
-You change entirely the system versions

ASSETS:
-Ownership of a customer. A telephone line for example

-