
sudo su - operation
>You enter operation mode in a linux server

4th server of sync1 is where we are at here.

There are some guidelines in the initial operations copypaste in the cmd


sudo /etc/init.d/osb_sync.sh *start* (or *stop*)


ps -ef 
>this shows all linux processes

ps -ef | grep weblogic
>takes the input from the left, puts it through the filter .
This will give us all the weblogic processes



OTHER DETAILS

Node Manager. Its a process required for Admin to run properly

Then there will be another gianormous process that is basically the server itself. Admin shuts down this part specifically

Lastly, itll catch grep itself as a command that is running.

