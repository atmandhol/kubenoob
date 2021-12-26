# KinD

`KinD` is a tool for running local Kubernetes clusters using Docker container “nodes”.
kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

Website: [https://kind.sigs.k8s.io/](https://kind.sigs.k8s.io/)

## Create a cluster

```
kind create cluster --name {name-of-cluster}
```

By default, the cluster access configuration is stored in `${HOME}/.kube/config` if `$KUBECONFIG` environment variable is not set.

If `$KUBECONFIG` environment variable is set, then it is used as a list of paths (normal path delimiting rules for your system). These paths are merged. When a value is modified, it is modified in the file that defines the stanza. When a value is created, it is created in the first file that exists. If no files in the chain exist, then it creates the last file in the list.

You can use the `--kubeconfig` flag when creating the cluster, then only that file is loaded. The flag may only be set once and no merging takes place.

## List all clusters

```
kind get clusters
```

More commands on the [Quick start](https://kind.sigs.k8s.io/docs/user/quick-start/) here.