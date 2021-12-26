# kubeconfig

The quickest, most efficient and widely used way to interact with a k8s cluster is using `kubectl` CLI. `kubeconfig` files are used to organize information about clusters, users, namespaces, and authentication mechanisms. The `kubectl` command-line tool uses kubeconfig files to find the information it needs to choose a cluster and communicate with the API server of a cluster.

A `kubeconfig` file has the following basic structure
```yaml
apiVersion: v1
kind: Config
preferences: {}

# List of clusters.
clusters:
- cluster:
    # Certificate authority file that the client can use to verify cert from the server
    certificate-authority: /path/to/ca-file
    # IP or host of the k8s cluster API server
    server: https://10.0.0.1/
    # Boolean flag that can be used to skip SSL/TLS
    insecure-skip-tls-verify: false
  name: development-cluster

# List of users and their creds.
users:
- name: developer
  user:
    # Option 1: Private key file and client certificate signed by certificate-authority
    client-certificate: /path/to/crt-file
    client-key: /path/to/key-file
    # Option 2: username/password. Not recommended over option 1 for obvious reasons.
    username: foo
    password: bar

# List of contexts. Context says which users can access which namespaces on what clusters.
contexts:
- context:
    cluster: development-cluster
    namespace: default
    user: developer
  name: dev
```

Look at the guide on [Configure Access to Multiple Clusters](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/) for learning commands on how to modify the kubeconfig files.

Once you have `clusters`, `users` and `contexts` set in the kubeconfig file, all the following setup is all based on `contexts`. There are commands in `kubectl config` CLI to switch contexts easily but it can get hard if you are dealing with a lot of clusters and contexts. 

```
$ kubectl config --help
  The loading order follows these rules:

  1.  If the --kubeconfig flag is set, then only that file is loaded. The flag may only be set once and no merging takes
place.
  2.  If $KUBECONFIG environment variable is set, then it is used as a list of paths (normal path delimiting rules for
your system). These paths are merged. When a value is modified, it is modified in the file that defines the stanza. When
a value is created, it is created in the first file that exists. If no files in the chain exist, then it creates the
last file in the list.
  3.  Otherwise, ${HOME}/.kube/config is used and no merging takes place.

Available Commands:
  current-context Display the current-context
  delete-cluster  Delete the specified cluster from the kubeconfig
  delete-context  Delete the specified context from the kubeconfig
  delete-user     Delete the specified user from the kubeconfig
  get-clusters    Display clusters defined in the kubeconfig
  get-contexts    Describe one or many contexts
  get-users       Display users defined in the kubeconfig
  rename-context  Rename a context from the kubeconfig file
  set             Set an individual value in a kubeconfig file
  set-cluster     Set a cluster entry in kubeconfig
  set-context     Set a context entry in kubeconfig
  set-credentials Set a user entry in kubeconfig
  unset           Unset an individual value in a kubeconfig file
  use-context     Set the current-context in a kubeconfig file
  view            Display merged kubeconfig settings or a specified kubeconfig file

Usage:
  kubectl config SUBCOMMAND [options]

Use "kubectl <command> --help" for more information about a given command.
Use "kubectl options" for a list of global command-line options (applies to all commands).
```


Fortunately, a handy little tool exists called [kubectx](https://github.com/ahmetb/kubectx). We are gonna use this tool to quickly change context for our `kubectl` CLI. Installation steps are in the repo. Since I have brew in my system, I am going to install it using
```
brew install kubectx
```
More info on usage for `kubectx` is [here](../../Projects-and-Tools/kubectx/).

!!! info "Order of KubeConfig"
    If you’re using kubectl, here’s the preference that takes effect while determining which kubeconfig file is used.

    - use --kubeconfig flag, if specified
    - use KUBECONFIG environment variable, if specified
    - use $HOME/.kube/config file

## Useful Links

- [Mastering the KUBECONFIG file](https://ahmet.im/blog/mastering-kubeconfig/)
- [Organizing Cluster Access Using kubeconfig Files](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/)
- [Configure Access to Multiple Clusters](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/)
- [kubectx](https://github.com/ahmetb/kubectx)
- [Cleanup dirty kubeconfig using kubeconfig-cleanup](https://github.com/ashleyschuett/kubeconfig-cleanup)