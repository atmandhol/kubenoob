# Networking in k8s
Excellent Video of Tim Hockin and Michael Rubin from Google explaining Networking basics of Kubernetes and how GKE (Google Kubernetes Engine) implemented it.
Link: [YouTube](https://www.youtube.com/watch?v=y2bhV81MfKQ&ab_channel=GoogleCloudTech)

## Components
- API Server - Kubernetes API Server
- Pods - Tiny VM like thing. Group of containers
	- everything inside a Pod shares a network. All localhost
- Controller - Piece of code that runs on the loop
	- Scheduler is a controller
	- Kubelet is a controller
	- Main job of a controller is to match reality with intent
- Labels
	- Key value pair. used to group things.
- Annotations
	- data that rides along with Object
- Selectors uses to point to label which eventually used to identify a group

## Basic Networking concepts in K8s
- Every pod has a real IP address (private) and its accessible to all other pods in the network
- Every pod gets its own namespace and network.
- Kubernetes expects that Pods must be reachable across VMs. It doesn’t care how.
- A `Service` is a group of endpoints. Service provides a stable Virtual IP (which does not change with changes in Pods). What changes is the IP mappings of the Pods to a service.
- `kube-proxy` is a controller that maintains the iptables it watches the API for service changes.
- `DNS` service helps resolving service names to Virtual IPs that are associated with the service. It is autoscaled based on the core counts and CPU counts.
- A `Service` is just and abstraction. Its a mapping of a name and IP to Pods that live in API server, but implementation is spread across all nodes and maintained by `kube-proxy`
- for L4 Load balancer, traffic from the client is just forwarded and the source ip is the client IP and the destination is LB.
- The `imbalance problem` is caused when there is no extra layer that distributes traffic to only the VMs that have the service pods.
- This can be solved by iptables. but it adds additional hops in the network and latency.
- NAT can happen for Source or Destination. calling it a SNAT or DNAT.
- annotation: `service.beta.kubernetes.io/external-traffic:OnlyLocal` for telling VMs to only use local pods and deal with imbalance. and this way, you can also have the client IP which is otherwise destroyed in the DNAT.
- Modern way of doing is as follows:

```yaml
spec:
  externalTrafficPolicy: Local
  type: LoadBalancer
```

- `Ingress` is for L7 load balancers. You need nodePort for this. What GKE does is that it allocates this port on all the nodes. Then using iptables, to transfer it to the right pod.