# kubectx

[kubectx](https://github.com/ahmetb/kubectx) is a tool to switch between contexts (clusters) on kubectl faster.
`kubens` is a tool to switch between Kubernetes namespaces (and configure them for kubectl) easily.

```
USAGE:
  kubectx                       : list the contexts
  kubectx <NAME>                : switch to context <NAME>
  kubectx -                     : switch to the previous context
  kubectx -c, --current         : show the current context name
  kubectx <NEW_NAME>=<NAME>     : rename context <NAME> to <NEW_NAME>
  kubectx <NEW_NAME>=.          : rename current-context to <NEW_NAME>
  kubectx -d <NAME> [<NAME...>] : delete context <NAME> ('.' for current-context)
                                  (this command won't delete the user/cluster entry
                                  that is used by the context)
  kubectx -u, --unset           : unset the current context

  kubectx -h,--help             : show this message
```

## Local setup for quick demo

- I have 2 kubernetes clusters running on my local.
    - First one is a `minikube` cluster. More info on how to [create a minikube cluster here](../../Local-Kubernetes/minikube/).
    - Second one is a `KinD` cluster. More info on how to [create a KinD cluster here](../../Local-Kubernetes/KinD/).

!!! important "Install FZF"
    fzf is a general-purpose command-line fuzzy finder.
    Github Repo: [https://github.com/junegunn/fzf](https://github.com/junegunn/fzf).
    It is installable via `brew`. It makes working with `kubectx` even better.


### Demo

- See all contexts and select.
```
$ kubectx
kind-test-cluster
minikube
```
