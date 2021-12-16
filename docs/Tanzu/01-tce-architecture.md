# TCE Architecture

For installation steps for Tanzu CLI, check the VMWare Tanzu Basics page.
Tanzu CLI is the best place to start. It can be invoked with `tanzu` command and it has commands related to Admin, Cluster management and System management.

## CLI
- The tanzu command is expected to be installed in machine’s path. 
- Each subcommand (binary) is expected to be installed in `${XDG_DATA_HOME}/tanzu-cli`
- on my linux mint, where I installed tanzu community edition using `brew`, the XDG_DATA_HOME is at `~/.local/share/`
- [Here is a list of where XDG_DATA_HOME resolves to](https://github.com/adrg/xdg#xdg-base-directory).
- Tanzu Community Edition ships with the tanzu CLI and a select set of plugins. 
- Some plugins may live in the `vmware-tanzu/community-edition` repository while others live in `vmware-tanzu/tanzu-framework`. 
- Plugins that live in community-edition is the free stuff that VMWare gives to users of TCE.
- Things in Tanzu Framework is for paid versions of platform and can have stuff promoted from TCE.
- [Carvel tools](../../Projects-and-Tools/carvel) comes as part of the Tanzu CLI.

## Managed Clusters
- Clusters that are deployed and managed using `tanzu cluster` command(s) are known as managed clusters.
- To bootstrap managed clusters, you first need a management cluster. that can be created by `tanzu management-cluster` commands.

## Standalone Clusters
- minikube competitor? maybe
- Clusters that run without a long-running management cluster are considered standalone clusters. Can be created using `tanzu standalone-cluster create`.

## Packages
- Tanzu Community Edition provides package management to users via the `tanzu` CLI. 
- Package management is defined as the discovery, installation, upgrading, and deletion of software that runs on Tanzu clusters.
- Each package is created using carvel tools. 
- Packages are put into a single bundle, called a package repository and pushed to an OCI-compliant registry. 
- Tanzu clusters comes installed with `kapp-controller` which is constantly watching for package repositories. 
- When a cluster is told about this package repository (likely via the `tanzu package repository` command), kapp-controller can pull down that repository and make all the packages available to the cluster.
- `kapp-controller` is installed in the Kubernetes cluster.

## TCE + BYOI (I is for Infrastructure)
- How does the managed clusters from TCE integrate with your preferred infrastructure?
- The Kubernetes image that gets deployed by Tanzu has some smarts in it. I will refer to that Kubernetes image as TKI.
- `ClusterAPI` is used to create a cluster in the actual infrastructure provider. Supported ones are AWS, Azure, VSphere and Docker (for local stuff).
- TKI worker nodes have 3 additional special processes that help with the integration.
    - CSI: Container Storage Interface: This driver is responsible for creating and attaching the storage to your kubernetes cluster.
    - CNI: Container Network Interface: This drivers help with [kubernetes networking](../../Basics/networking/) between pods. TKI comes installed with Antrea and Calico.
    - CPI: Cloud Provider Interface: for Cloud based Load balancing.
- TKI comes installed with [External DNS](https://github.com/kubernetes-sigs/external-dns)
- Its a project that can automatically add DNS records to your DNS provider of your choice as the services are created/destroyed in the TKI based cluster.
- All of this is done declaratively using Kubernetes YAML.
- How do you make sure your Kubernetes cluster is up to the spec with official Kubernetes specification? You run something called a `Conformance test`. [`Sonobuoy`](https://sonobuoy.io/) is a built in tool in TKI that can run Conformance testing to ensure that a cluster is properly configured and that its behavior conforms to official Kubernetes specifications.

## TCE + Consistent App Deploys
- The Conformance testing using `Sonobuoy` helps make sure that the Cluster is up to the spec.
- Carvel Package Management tools can help with consistently deploying/upgrade apps on the Kubernetes cluster in form of packages.
- TKI comes built with [`Harbor`](https://goharbor.io/) container registry.
- TKO comes installed with powerful packages like `Knative` or `Contour` L7 LB serving.

## TCE + Security
- `Velero` comes pre-installed as package for DR and Backup to S3 features.
- VMWare Base Image for TKI is signed and secure.
- TKI comes installed with [`cert-manager`](https://cert-manager.io/) package, the gold standard for x.509 cert management for Kubernetes for encrypting inter-service communications.
- [`Harbor`](https://goharbor.io/) container registry comes with some very powerful vulnerability scanning at the image level.
- You can set policy to not allow pulls for messed up images with Critical vulnerabilities.
- [`Pinniped`](https://pinniped.dev/) package comes built in with TKI, and can help with seamless Authentication with LDAP and OIDC based providers.

## TCE + Obervability
- `Grafana`, `Prometheus` and `Fluentbit` can all be installed as packages which is pretty much all you need for most application workloads to visualize how things are going.

## Video Links
- [Getting started with Tanzu Community Edition](https://www.youtube.com/watch?v=UnxQjhXb2K4&ab_channel=VMwareTanzu)