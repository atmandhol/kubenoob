Minikube is a k8s SIG Project. SIG stands for Special interest group. [Minikube website is here](https://minikube.sigs.k8s.io/docs/). minikube quickly sets up a local Kubernetes cluster on macOS, Linux, and Windows. We proudly focus on helping application developers and new Kubernetes users.

To get started, you can refer to their [basic controls docs page](https://minikube.sigs.k8s.io/docs/handbook/controls/).

## Local Setup using Minikube
I am running all this on a macOS, so all the intructions will be for Macs. But I will link installations for other OS if available on the product page. [Installation page for minikube is here](https://minikube.sigs.k8s.io/docs/start/).

- Install minikube using `brew install minikube`
- Install hyperkit for VM runtime `brew install hyperkit`

HyperKit is a toolkit for embedding hypervisor capabilities in your application. It includes a complete hypervisor, based on xhyve/bhyve, which is optimized for lightweight virtual machines and container deployment. It is designed to be interfaced with higher-level components such as the VPNKit and DataKit.
HyperKit currently only supports macOS using the Hypervisor.framework. It is a core component of Docker Desktop for Mac. [Github repo for hyperkit is here](https://github.com/moby/hyperkit)

- minikube also installs `kubectl` which is the CLI for interacting with Kubernetes
- to start minikube with hyperkit use
-> `minikube start —-vm-driver=hyperkit`
-> `minikube status` to check if everything is up fine

### minikube supported runtimes
Container or virtual machine manager, such as: Docker, Hyperkit, Hyper-V, KVM, Parallels, Podman, VirtualBox, or VMware Fusion/Workstation