
## Section 11 - Getting Started with Kubernetes


Pod
- Contains, manages, and executes at least one container.
- Can be thought of as the smallest possible unit you can define, in a configuration file, for Kubernetes to create.
- Run inside a Worker Node

Worker Node
- Can be thought of as your machine or virtual instances.
- Run the containers of your application.
- 1 or more pods can run on the same worker node.

Kubernetes needs a **Proxy** to control the network traffic on the node.
- The proxy controls where the pods can reach the internet and how the pods (and the containers running inside of them) can be accessed from the outside world.

Master Node
- A Control Plane running on the Master Node creates, replaces, and shuts down worker nodes to scale up or down with load.
- You don't interact directly with the Control Plane
- Many master nodes may exist across multiple machines to ensure high availability.



## Section 12 - Kubernetes in action

### Section 184 - Required Setup & Installation Steps
Requirements:
- A Cluster
	- A Master Node
	- 1+ Worker Nodes
		- All "software", or services, installed
- kubectl tool
	- https://kubernetes.io/docs/tasks/tools/
	- used to send instructions to a cluster
		- create a deployment
		- change a deployment
		- delete a deployment
	- Used to send instructions to the master node, which will do what it needs to with the worker nodes.

Use minikube to learn how to use Kubernetes
- https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Farm64%2Fstable%2Fbinary+download

sysctl -a | grep -E --color 'machdep.cpu.features|VMX'

`minikube start --driver=docker`



### Section 187 - Understanding Kubernetes Objects

Kubernetes works with objects:
- Pods
- Deployments
- Services
- Volume
- and more...

Objects may be declared Imperatively or Declaratively

### The "Pod" Object
- Has its own internal IP address, but it changes and is manages by a service (see below).

### The "Deployment" Object
(The Main Kubernetes Object)
- you tell a deployment how many pods and containers it should manage for you.
- can control one or multiple pods
- Set a desired target state: e.g., 2 pods with this container up & running, and Kubernetes will try to reach the target state.
- Kubernetes will place the pods on worker nodes that have sufficient memory and CPU capacity for new pods, we don't need to manually pick a machine.
- may pause, delete, rollback a failing deployment and go back to a previous working deployment.

Use the `kubectl` command to create a new deployment object (Imperative Approach):
- `kubectl create deployment <deployment name> --image=<which image to use for the container of the pod created by this deployment>`
	- NOTE The image needs to be available within the cluster. If it isn't you'll get an `ErrImagePull` error status. You can get the status with `kubectl get pods`.

One way to make the image available within the cluster:
1) Sign into [Docker Hub](https://hub.docker.com) in a browser.
2)  Create a new docker hub repository.
3) (if needed) (Re)tag the image on you machine that you want to deploy.
	- `docker tag <image name> <docker hub account name>/<repository name>`
	- E.g., `docker tag kub-first-app academind/kub-first-app`
4) Log into Docker (You will be prompted for a username and password)
	- `docker login`
5) Push the image to Docker Hub
	- `docker push <docker hub account name>/<repository name>`
	- E.g., `docker push academind/kub-first-app`
	- The image can now be accessed anywhere in the world, including by our cluster.
6) Create the deployment from the ==remote== repository (Docker Hub)
	- `kubectl create deployment <deployment name> --image=<docker hub account name>/<repository name>`
	- E.g., ``kubectl create deployment --image=academind/kub-first-app`

See how many Deployments are connected to our cluster:
(The "READY" column shows how many deployments are ready as a fraction of the total that are supposed to be ready.)
- `kubectl get deployments`

DELETE a Deployment:
- `kubectl delete deployment <deployment name>`

See all the pods created by our deployments:
- `kubectl get pods`

>Using Kubernetes API Proxy to access a Remote Dashboard
>
>You can also access the dashboard via the Kubernetes API server proxy.
>1. **Start the Proxy** on the remote server:
>   `kubectl proxy --address='0.0.0.0' --accept-hosts='^.*$'`
>2. Access the Dashboard: Go to `http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/` on your local machine’s web browser.

### The "Service" Object
To reach a Pod and a container running within it, we need a Service object.
- Exposes Pods to the cluster or Externally
- Groups pods together and gives them a shared IP address that doesn't change
	- The IP address can be exposed inside the cluster and externally.
	- The default is internal access only.

We can create a service with `kubectl create service`, but a more convenient way to expose a pod created by a deployment is to use the `kubectl expose` command.
- `kubectl expose deployment <deployment name> --type --port=<port the container listens on>`
- E.g., `kubectl expose deployment first-app --type=LoadBalancer --port=8080`
	- cluster types
		- ClusterIP - Only reachable within the cluster.
		- NodePort - Indicates that the deployment should be exposed with help of the IP address of the worker node on which it is running.
		- LoadBalancer - Generate a unique IP address and evenly distribute incoming traffic across all pods that are part of this service.
			- AWS and Minikube support LoadBalancer

Confirm a Service was created:
- `kubectl get service`
	- If deploying on a cloud provider, there would be an external IP
	- In Minikube, the External IP will remain in the Pending status.
		- Minikube command to Map a port to an IP address we can access from our local machine, which identifies the virtual machine running on the local machine.
		- `minikube service <deployment>`



>To access the page served by Minikube on a remote headless server via SSH tunneling, you'll need to forward the port on your local machine to the port on the remote server where Minikube is serving the page.
>
>Here's how you can do it:
> Command Breakdown:
>
>1. **SSH command**:
>    
	 `ssh -L 8001:192.168.49.2:32475 user@remote_server_ip`
	 `ssh -L 8001:192.168.49.2:32475 **machine@raspberrypi.local`
>    
    - **`-L 8001:192.168.49.2:32475`**: This specifies that traffic sent to `localhost:8001` on your local machine will be forwarded to `192.168.49.2:32475` on the remote server.
        - `8001`: The local port on your machine that you'll use to access the page.
        - `192.168.49.2`: The IP address of the Minikube cluster on the remote server.
        - `32475`: The port on which Minikube is serving the page.
>
    - **`user@remote_server_ip`**: The SSH connection to the remote server, where `user` is your username and `remote_server_ip` is the IP address or domain of the server.
>
> Steps to Access the Page:
>
>	1. **Run the SSH command** on your local machine:
>    
> 	   `ssh -L 8001:192.168.49.2:32475 user@remote_server_ip`
> 		   
>	2. **Open your web browser** on your local machine and go to:
>    
> 	   `http://localhost:8001`
>
    This will forward the request through the SSH tunnel to the Minikube page served at `192.168.49.2:32475` on the remote server.


### Section 189 - A First Deployment - Using the Imperative approach

==I know this is redundant==

1. Build the image:
```
docker build -t kub-first-app .
```

2. Check whether the cluster is up and running:
```
minikube status
```

2. (B) Start the cluster if necessary:
	- Setting the driver to docker uses docker to create a virtual containerized environment, which we're simulating on our local machine, to then task kubernetes, which is all about containers...
```
minikube start --driver=docker
```

3. Create a repository for images
4. (Re)tag the docker image.
```
docker tag <image name> <Repository account name>/<repository name>
```
E.g.,
```
docker tag kub-first-app academind/kub-first-app
```
5. Push the tagged image to the repo (e.g., DockerHub):
	- This makes the image available anywhere in the world over the internet, including from your cluster.
```
docker push academind/kub-first-app
```

1. Send an instruction to create a deployment to the cluster:
	- The image is not taken from the local machine and sent to the virtual machine. The command is sent to the kubernetes cluster, and the cluster will then look for the image, so point to an image registry like DockerHub.
	- E.g., point to `dariobianco/kub-first-app` on DockerHub, not `kub-first-app` on your local machine.

```
kubectl create deployment first-app --image=dariobianco/kub-first-app
```


```
kubectl get deployments
```

| NAME      | READY   | UP-TO-DATE | AVAILABLE | AGE |
| --------- | ------- | ---------- | --------- | --- |
| first-app | ==0/1== | 1          | 0         | 27s |
- `0/1` in the READY column indicates that we have 1 deployment and 0 of them are ready.
- This means 1 deployment or 1 deployments failed.
- \<Current State>/\<Target State>

See pods created by deployment
```
kubectl get pods
```

| NAME      | READY   | STATUS       | RESTARTS | AGE |
| --------- | ------- | ------------ | -------- | --- |
| first-app | ==0/1== | errImagePull | 0        | 60s |
