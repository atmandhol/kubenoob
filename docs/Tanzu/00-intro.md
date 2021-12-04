# VMWare Tanzu Basics

Tanzu is a suite of products that helps users run and manage multiple Kubernetes (K8S) clusters across public and private “clouds”. While introducing Kubernetes as a first class VMware product, it still keeps strong ties to the VMware virtualization portfolio.

- [Why Tanzu?](https://tanzu.vmware.com/why-tanzu)
- [Tanzu Modern Apps](https://tanzu.vmware.com/modern-apps)

But the most interesting thing for me, is [Tanzu Community Edition](https://tanzucommunityedition.io/) cause I like free stuff. Who doesn't?

## Tanzu Community Edition (TCE)

VMware Tanzu Community Edition is a full-featured, easy to manage Kubernetes platform for learners and users. It is a freely available, community supported, open source distribution of VMware Tanzu that can be installed and configured in minutes on your local workstation or your favorite cloud. [Learn more about it here](https://tanzucommunityedition.io/docs/latest/).

Here is the [Github Repo for Community Edition](https://github.com/vmware-tanzu/community-edition). The README has installation steps using package manager and manual installation steps as well. Download it from [here](https://tanzucommunityedition.io/download/). I am using macOS so I'll download that and use that.

### Install using Brew

- Run Homebrew install
```
brew install vmware-tanzu/tanzu/tanzu-community-edition
```

- To do this, you are also gonna need the latest xcode tools on macOS. You can do that using the following commands
```
sudo rm -rf /Library/Developer/CommandLineTools
sudo xcode-select --install
```
A popup will appear, click the install button. It is a big-ass download and will take a while to install so make some coffee or popcorn.


- To initialize all plugins required by Tanzu Community Edition, an additional step is required. To complete the installation, please run the following shell script:
```bash
sh /usr/local/Cellar/tanzu-community-edition/v${version}/libexec/configure-tce.sh
```

- To cleanup and remove Tanzu Community Edition from your system, run the following script:
```bash
sh /usr/local/Cellar/tanzu-community-edition/v${version}/libexec/uninstall.sh
```

!!! note "Important"
    Replace ${version} with the version of Tanzu Community Edition you installed in the above commands.

## Tanzu Built-in Packages

Tanzu Community edition comes with a bunch of goodies a.k.a. `packages`. [List of all those packages are here.](https://github.com/vmware-tanzu/community-edition#packages)