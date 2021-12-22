# Container Basics

Detailed Article explaining [the differences between Docker, containerd, CRI-O and runc](https://www.tutorialworks.com/difference-docker-containerd-runc-crio-oci/)

## Tools
    - Docker
    - Kubernetes

## Container Runtimes
CRI - Container Runtime Interface is the kubernetes API that tells how to interact with the container runtime

	- containerd - from Company Docker
	- CRI-O - from Red Hat

## Open Container Initiative (OCI) Spec
	- Both container runtimes uses it
	- Also provides implementation details of runc
	- runc is used to start the container

## Docker
Docker tool (CLI, etc. that talks to the daemon) -> containerd -> calls runc (OCI spec) -> creates container

- Dockershim is Kubernetes thing which allows it to support docker.
- Kubernetes prefers to run containers through any runtime that supports CRI
- But docker is older than kubernetes, that is why docker shim exists.

- Docker images
	- are actually OCI compliant packaged images

