### Namespace 
-You run a batch script
	-You make the script think its alone in a whole operating system. This is called a
	## NAMESPACE

### Docker 
-Has a scripting language which made it so popular.
-Has a Container Engine

## in linux
APP 1        APP 2       APP 3 
BINS/LIB    BINS.LIB   BINS.LIB
C O N T A I N E R E N G I N E 
O P E R A T I N G S Y S T E M 
	   **INFASTRUCTURE**

## in windows

--APP 1        APP 2       APP 3--
--BINS/LIB    BINS.LIB   BINS.LIB--
--C O N T A I N E R E N G I N E--
	--L I N U X   O    S--
	--H Y P E R V I S O R--
--O P E R A T I N G S Y S T E M--
	--**INFASTRUCTURE**--


### WHY NEED KUBERNETES

-We want much more control over our services and processes.


### KUBERNETES CLUSTER
(how kubernetes is managed)

-DESIGN
	-API server. 
	-  c-m: Its a controller that makes sure things work exactly according to the developer's configs
	- c-c-m: Optional. Cloud controller. Ote doesnt use this
	- sched (scheduler): Schedules where a new ylopoihsh will go on which nodes/slaves.
	- etcd: A key value store. All configs, all data are in here.
	  c-m uses all its data from here.
	  ITS THE MOST INTEGRAL COMPONENT and can be put in another server for security reasons, and with backups.
		  -If its deleted, workers will continue to work but they can't be controlled anymore.
	-There is OTHER components but these are the MOST ESSENTIAL
	  
-ONE ACTIVE MASTER AT A TIME

-NODES 
	-Kubelet: This communicates with the Master.
	-Kubernetes-Proxy: Network connection with Master and other Workers.

### GENERAL FLOW 

HELM SENDS YAML TO API>
	API TURNS IT INTO JSON. SENDS IT TO C-M OR
	SCHEDULER > TO APPLY IT 
HOW IS THE YAML WRITTEN?
	-Manual (semi. You config a default file you're given)
		Not necessary usually.
	-Preconfigured. These usually exist already for big projects


### KUBERNETES TERMINAL

-**kubectl** (comes from kubernetes control) 
	-We have access via a script that uses our groupnet credentials
-pk-smaster.cosmote.gr is a fake address. Just tells you you are connected to the Master of the Kubernetes
-Ideally every microservice goes through Kubernetes, but this wasn't true at the time. Most did though.


COMMANDS
-edit
	-Heads up: **CICD of Jenkins** is what's normally managing the code. 
	Each team has its own Jenkins, tho they are all the same. It uses a tool called **HELM** to do the deployments to Kubernites
	- Never use this unless you are super duper careful.
	 You can edit the -yaml of a deployment, and to add replicas live. Then it must be edited in GITLAB so that we know what code we have inside the live deployment.
-get
	-get nodes: gets us our nodes
	-get nodes -o wide: same but more information
		--Here we see IPs of nodes etc etc.
		--Each here is a docker image
		--Random fact: google doesn't use docker anymore.
	-get namespaces: shows the processes running
	-get ns (same as namespaces)
	-n prod-name get pods
		-gets you pods
	-get resourcequotas -n your_service_name
		 --shows resources available and used
		 --Fact: Kubernetes splits each cpu into many tiny pieces. If you see something like 11300m used, its like 11.3 cores. It's divided by a thousand. so 10 cores is 10000 cores in kubernetes.
	-get deploy
		--gets you deployments
-api-resources (IMPORTANT)
	-api-resources: gives us a list of all requests we can make
	 for example. namespaces

	
	
-describe
	-describe resourcequotas -n prod-bre mem-cpu-quota
		--works like get resourcequotas but is more specific and "the correct way"
		--here, namespace = prod-bre, and name = mem-cpu-quota

##### POD
- A pod is the smallest unit of measurement in a Kubernites in terms of code execution
- They think they are alone in the OS
- They can't run most things by themselves
- Microservice management is done thanks to other infastructures, most famous being Deployments
	- -n prod-bre  get deployment c1ng-deployment -o yaml
		- We can see the settings of the particular deployment . The most important:
		- namespace: prod-bre
		- name: c1ng-deployment
		- labels: app: c1ng
			- This is a core method of how Kubernites works. 
			- matchLabels: app: c1ng. This is how it decides to ACTUALLY select and run c1ng
			- VERY IMPORTANTE!!!! 111 !!!!
			- Dynatrace does not recognize labels from resources....At least it didnt back then
		- kind: deployment
		- replicas: 2 
			- this is important. This means 2 pods are handling this Deployment
		- Container: -
			- this is the code the pods contain.
		- readinessProbe 
			
		- livelinessProbe
			- path: /o2b/c1ng/v1.0/actuator/health
				- periodSeconds: 10
					- check every 10 seconds if its live
				- InitialDelay:140
					- on startup delay checks for 140 seconds
		- ReadinessProbe (good for sitescope checks)
			- failureThreshold: 10
				- tells you if its up and running. The kybernite will restart the process if either this or the liveliness periodSeconds detects its not running
		- limits
			- cpu: 800m: I am changing format from the indented bulletpoints
			 The maximum amount of cpu dedicated.
			 
			- RESOURCE QUOTAS, LIMITS, REPLICAS are the 3 limiters on resources.
				- THIS IS ALL PER CONTAINER
		- requests:
			-cpu: 200m. Also important. Low requests high limits is something you'll see.
		- On requests and limits:
			- Two replicas with 800m cores each, is 1.6 cores each. 
			- We configure the Kubernite to draw memory and cores as needed, depending on the load. 
- horizontalpodautoscalers also known as hpa
	- This handles the amount of replicas active at a time depending on the load:
	 - Minpods: Minimum Pods
	 - Maxpods: Maximum Pods
	 - Replicas: Active pods
	 - Targets: Its when the process will decide to upscale
	   For example. For 70% Target, If ONE of the pods hits 70%, then it'll add another replica
	 - THERE IS other variants of hpa. There is stuff like requestsPerSecond etc.
	 - The pods are downed/withdrawn when usage is down, starting from the latest pod that was erected. 

- ABOVE POD, THERE IS ANOTHER entity called Replica Set
	- The only thing Replica Set does, is to contain the Replicas.
	- Naming scheme of pods:  auth-675446675c-9xcmm
		- auth is the deployment name
		- 675446675c is the Replica Set name. Its rng
		- 9xcmm is the name of the pod. Also rng
		- 
- MASTERS CAN ALSO RUN PODS, But we avoid doing that
- YOU CAN TELL WHAT TYPE A POD IS BY ITS NAMING SCHEME
	  For example: jenkins-679945588d-lws22 is a regular pod
	  If it was jenkins-lws22 it'd be a Daemonset pod
	  If it was jenkins-1 it'd be a stateful set 

#### DAEMONSETS
-Sometimes we want just ONE pod in every node of a Kubernite.
- Uses? Lets say I want to depoy Filebit in the Kubernete
- We want logs from every node. We want pods in all the nodes at once to do that. 
- As you understand, this is mainly best used for Monitoring tools.
- THESE RUN ALSO ON MASTERS. It is necessary when it comes to Daemonsets
- Daemonsets do not have liveliness and readinessProbes
  They work automatically. 
  They run a set of lower level code to be controlled automatically.
- Pods that run under a Daemonset have no Replica set name. They are named like filebeat-4ghkg . 

### STATEFULSET

- n -prod-mongopt get statefulset (example of getting a stateful set)
 - What is a stateful set? Its like a Deployment for pods, but unlike a deployment, each Pod has a unique identifier and handles something different.
 - They are not equal .
 - Volume space is not deleted when the Statefulset is downsized to avoid data-loss
 - To successfully remove all pods, we are allowed to downscale them to 0 first before deletion. Otherwise we may have remnants of this deployment.
 - we can code stateful sets for the pods to get themselves up with a particular delay and order. 
 - pod 0 is the Master. Always.
 - mongo: 
	 - mongopt is a database inside kubernetes. every pod is an instance of the database
	 -  mongopt is a stateful set in our system
	 - each pod is a copy of the database. each instance of the database increases performannce.
	 - This requires a Filesystem to keep mongo inside
	 - The storage / data for mongo is OUTSIDE Kubernetes with NFS. 
 - storageClassName: mongo:
	 - This is like a label. It names the storage. 
	 - 

#### PERSISTENT VOLUMES/ STORAGE
 
 - There are 3 Filesystems, for the 3 pods of Mongo outside of Kubernetes
		 - They are called PERSISTENT VOLUMES
		 - They don't belong to a namespace, they belong to the CLUSTER
		 - To view them, we use " get pv" 
		 - ClaimRef: nfs: path /k8s-jenkins is an example path of a storage. (storage in name pv-protection)
		 - containers.volumeMounts.readOnly = true with ReadWriteOnce on pods you want only read access
	- You do not need to be a database to require storage. You could be exporting files like xlsx
	- Many pods can reserve the same persistent volume. Its reserved by a persistent volume claim.

We set the NFS by setting up a persistent volume.
Then we make a persistent volume CLAIM of a certain size. Then if it finds it it goes and claims it.
The pod stilll cannot see the space. 
In the volumes section, 


#Dynatrace
[Dynatrace]  
#### Dynatrace and Kubernetes

We first have the k8 cluster. It is the production cluster of...clusters
	- Under Cluster, follow the workers
	- Workers are physical servers
	- On those physical servers/workers, we got the namespaces
	- A namespace is made out of workloads. (Deployments)
	- Namespace - Microservice/Workload/Deployment - Pod - Controller- Service  
		-We can have one or many controllers. They are parts of code
		-Inside of Controllers are Services.
		-The Balancers are handled by Kubernetes, those are outside of this process.
		