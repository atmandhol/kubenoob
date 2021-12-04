# Components in k8s Cluster

When you deploy Kubernetes, you get a cluster.

A Kubernetes cluster consists of a set of worker machines, called nodes, that run containerized applications. Every cluster has at least one worker node.

## Primary components

The worker node(s) host the Pods that are the components of the application workload. The control plane manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.

Checkout the [Kubernetes Documentation on various components that make a cluster here](https://kubernetes.io/docs/concepts/overview/components/).

Also definitely checkout this excellent and very detailed video by `Nana Janashia` on her Youtube channel `TechWorld with Nana` to learn the basics of Kubernetes and to get started. [YouTube Video Link](https://www.youtube.com/watch?v=X48VuDVv0do&ab_channel=TechWorldwithNana). 

## What is Kubernetes and why you need it?
Kubernetes is a container orchestration tool that does 3 things.

- High Availability
- Scalability
- Disaster Recovery

## Kubernetes Components
### Pods
- Abstraction over container
- Usually 1 app per pod
- Each pod gets its own IP
- New IP on re-creation

### Service
- Permanent IP address
- Also acts as a load balancer between replicas
- Lifecycle of Pod and Service not connected
- Can be of 2 type. 1) External and 2) Internal based on connectivity from the internet

### Ingress
- Assigns custom Domain to a service

### ConfigMap
- External config of your app. e.g. Environment variables 

### Secrets
- Used to store secret data, base 64 encoded

### Volumes
- Storage on local nodes or external
- Kubernetes does not manage data persistence on disks

### Deployments
- Blueprint of Pods. Provides an abstraction layer
- Like Task Definition in AWS
- Only useful for Stateless apps

### Replicasets
- are logical abstractions created while creating a deployment

### Stateful Sets
- Used for hosting Stateful apps like DB
- Although, best practices suggests DB are hosted outside of Kubernetes

## Types of Compute Nodes
Nodes are machines. VMs on Cloud, on-premise, your local computer etc.

### Worker Nodes
- each node has multiple pods in it
- worker nodes do all the work so more CPU and RAM is given to these
- every worker node has 3 processes
	- `Container runtime`. e.g. Docker, container
	- `Kubelet`. is a controller and a Main process that talks to container runtime and create/remove pods. It also talks to Controller manager.
	- `Kube Proxy` manages connection between nodes and transfers commands to Kubelet

### Master Nodes
Are the nodes that maintains the cluster state

- every master node runs 4 processes
	- `API Server`  acts as a cluster gateway and gatekeeper for authentication
	    - it is distributed and load balanced across master nodes
	- `Scheduler`  decides on which node, new pods should be scheduled
	    - New pod request -> API server -> Scheduler -> Kubelet
	- `Controller manager`  detects cluster state changes
	    - Controller manager -> Scheduler -> Kubelet
	- `etcd` is the cluster brain. the key value pair store which is distributed across master nodes

## Local setup
- Checkout my Notes on the `Local Kubernetes` Section of this docs to learn various ways to run k8s locally.

## Kubectl commands
### `get`

- get nodes, pods, deployments, services, replicasets
- use `-o wide` to get even more info
- use `-o yaml` to get the output in yaml format
- `kubectl get all` gets you all the components

### `create`
- create deployment
	- `kubectl create deployment {name} —image={docker-image}`
	- Just need name and image. rest is default
	- creates a replicaset
	- Deployment manages -> replicaset manages -> pods contains -> container

### `edit`
- edits deployment
	- `kubectl edit deployment {name}`

### `logs`
- logs what the pod logs
	- `kubectl logs {pod name}`

### `describe`
- describes a pod
	- `kubectl describe {pod name}`

### `exec`
- SSH into the pod
	- `kubectl exec  -it. {pod name} -- bin/bash` 

### `delete`
- deletes a deployment

### `apply`
- applies a configuration file
	- `kubectl apply -f {file.yaml}`
- apply knows whether to create or update an deployment

## Kubernetes YAML file
4 parts of configuration file

- type declaration
	- apiVersion
	- kind

- metadata
	- name
	- labels `defines the tag for the deployment`

- spec (desired)
	- specific to kind
		- replicas
		- selector `tells what dad component this belong to`
		- template
	`This is at Pod level`
			- metadata
			- spec
				- containers
					- name
					- image
					- ports
						-  `should match service.ports.port`
						- containerPort
					- env
						- name
						- value		
		- ports
			- protocol
			- targetPort
			- port

- status (actual)
	- status of the running cluster. this data is used as a basis
	- this data is stored in etcd

- Best practice is to store YAML templates with your code
- Labels are global in namespace

## Sample YAML files
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: proxy
  labels:
    component: proxy
spec:
  replicas: 2
  selector:
    matchLabels:
      component: proxy
  template:
    metadata:
      labels:
        component: proxy
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 8080
		  env:
        - name: foo
          value: bar

```

```
apiVersion: v1
kind: Service
metadata:
  name: proxy-service    
spec:
  selector:
    component: proxy
  type: LoadBalancer     # this makes an external service
  ports:
  - protocol: TCP
    # is for internal communication
    port: 80
    targetPort: 8080
    # this is for external communication
    nodePort: 30000-32767 

```

```
apiVersion: v1
kind: Secret
metadata:
  name: mongodb-secret
type: Opaque   
data:
  username: base64 encoded
  password: base64 encoded

```

- For assigning external IP in minikube use
	`minikube service {service-name}`


## Internode communication

Learn more about the [Control Plane - Node Communication and Hub & Spoke API pattern here](https://kubernetes.io/docs/concepts/architecture/control-plane-node-communication/).
