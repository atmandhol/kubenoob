# Hands-on TCE

## Deploy a Management Cluster Locally

- To Create clusters using TCE, you first need a management cluster. This cluster is then used to bootstrap managed clusters.

```
$ tanzu management-cluster create --ui
```

- This command launches an installer UI that gives you infrastructure choices on where you want to deploy your management cluster.

- Every infrastructure provider will have a different set of requirements to get the cluster up and running. I choose Docker so that cluster can be installed on my local workstation.

![Step 1](../../images/step1-docker.png)
![Step 2](../../images/step2-docker.png)
![Step 3](../../images/step3-docker.png)
![Step 4](../../images/step4-docker.png)

??? info "Sample Management Cluster Creation log"
    ```yaml
    ℹ [1217 10:15:14.13476]: logger.go:115] Preparing nodes ...
    ℹ [1217 10:15:16.71979]: logger.go:115] Writing configuration ...
    ℹ [1217 10:15:17.29959]: logger.go:115] Starting control-plane ...
    ℹ [1217 10:15:38.53773]: logger.go:115] Installing CNI ...
    ℹ [1217 10:15:39.09041]: logger.go:115] Installing StorageClass ...
    ℹ [1217 10:15:39.63233]: logger.go:115] Waiting 2m0s for control-plane = Ready ...
    ℹ [1217 10:16:04.71014]: logger.go:115] Ready after 25s
    ℹ [1217 10:16:05.32815]: init.go:176] Bootstrapper created. Kubeconfig: /home/atmandhol/.kube-tkg/tmp/config_ajGrOAGE
    ℹ [1217 10:16:05.35695]: init.go:188] Installing providers on bootstrapper...
    ℹ [1217 10:16:33.82480]: init.go:482] installed Component=="cluster-api" Type=="CoreProvider" Version=="v0.3.23"
    ℹ [1217 10:16:33.82482]: init.go:482] installed Component=="kubeadm" Type=="BootstrapProvider" Version=="v0.3.23"
    ℹ [1217 10:16:33.82487]: init.go:482] installed Component=="kubeadm" Type=="ControlPlaneProvider" Version=="v0.3.23"
    ℹ [1217 10:16:33.82488]: init.go:482] installed Component=="docker" Type=="InfrastructureProvider" Version=="v0.3.23"
    ℹ [1217 10:16:33.92911]: init.go:651] Waiting for provider cluster-api
    ℹ [1217 10:16:33.94062]: init.go:651] Waiting for provider infrastructure-docker
    ℹ [1217 10:16:33.94065]: init.go:651] Waiting for provider control-plane-kubeadm
    ℹ [1217 10:16:33.94062]: init.go:651] Waiting for provider bootstrap-kubeadm
    ℹ [1217 10:16:34.01156]: clusterclient.go:1105] Waiting for resource capd-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:16:34.11995]: clusterclient.go:1105] Waiting for resource capi-kubeadm-control-plane-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:16:34.26535]: clusterclient.go:1105] Waiting for resource capi-kubeadm-bootstrap-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:16:34.39119]: clusterclient.go:1105] Waiting for resource capi-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:16:39.29643]: clusterclient.go:1105] Waiting for resource capi-kubeadm-bootstrap-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:16:39.30218]: init.go:659] Passed waiting on provider bootstrap-kubeadm after 5.361576168s
    ℹ [1217 10:16:44.17337]: clusterclient.go:1105] Waiting for resource capi-kubeadm-control-plane-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:16:44.18087]: init.go:659] Passed waiting on provider control-plane-kubeadm after 10.240216455s
    ℹ [1217 10:16:44.45769]: clusterclient.go:1105] Waiting for resource capi-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:16:49.47260]: init.go:659] Passed waiting on provider cluster-api after 15.543560254s
    ℹ [1217 10:17:14.11307]: init.go:659] Passed waiting on provider infrastructure-docker after 40.17245036s
    ℹ [1217 10:17:14.11309]: init.go:670] Success waiting on all providers.
    ℹ [1217 10:17:14.11314]: init.go:202] Start creating management cluster...
    ℹ [1217 10:20:00.47511]: clusterclient.go:1257] Getting secret for cluster
    ℹ [1217 10:20:00.47514]: clusterclient.go:1105] Waiting for resource tce-mgmt-cluster-kubeconfig of type *v1.Secret to be up and running
    ℹ [1217 10:20:00.48436]: init.go:234] Saving management cluster kubeconfig into /home/atmandhol/.kube/config
    ℹ [1217 10:20:00.50239]: init.go:257] Installing providers on management cluster...
    ℹ [1217 10:24:50.31598]: init.go:482] installed Component=="cluster-api" Type=="CoreProvider" Version=="v0.3.23"
    ℹ [1217 10:24:50.31606]: init.go:482] installed Component=="kubeadm" Type=="BootstrapProvider" Version=="v0.3.23"
    ℹ [1217 10:24:50.31652]: init.go:482] installed Component=="kubeadm" Type=="ControlPlaneProvider" Version=="v0.3.23"
    ℹ [1217 10:24:50.31669]: init.go:482] installed Component=="docker" Type=="InfrastructureProvider" Version=="v0.3.23"
    ℹ [1217 10:24:59.94350]: init.go:651] Waiting for provider control-plane-kubeadm
    ℹ [1217 10:24:59.94351]: init.go:651] Waiting for provider bootstrap-kubeadm
    ℹ [1217 10:24:59.94372]: init.go:651] Waiting for provider cluster-api
    ℹ [1217 10:24:59.94375]: init.go:651] Waiting for provider infrastructure-docker
    ℹ [1217 10:24:59.97631]: clusterclient.go:1105] Waiting for resource capd-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:25:00.05886]: clusterclient.go:1105] Waiting for resource capi-kubeadm-control-plane-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:25:00.06354]: clusterclient.go:1105] Waiting for resource capi-kubeadm-control-plane-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:25:00.06969]: init.go:659] Passed waiting on provider control-plane-kubeadm after 124.87846ms
    ℹ [1217 10:25:00.10639]: clusterclient.go:1105] Waiting for resource capi-kubeadm-bootstrap-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:25:00.11835]: clusterclient.go:1105] Waiting for resource capi-kubeadm-bootstrap-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:25:00.12754]: init.go:659] Passed waiting on provider bootstrap-kubeadm after 185.141542ms
    ℹ [1217 10:25:00.16960]: clusterclient.go:1105] Waiting for resource capi-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:25:00.17474]: clusterclient.go:1105] Waiting for resource capi-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:25:00.17778]: init.go:659] Passed waiting on provider cluster-api after 235.685059ms
    ℹ [1217 10:25:05.00344]: init.go:659] Passed waiting on provider infrastructure-docker after 5.061054978s
    ℹ [1217 10:25:05.00350]: init.go:670] Success waiting on all providers.
    ℹ [1217 10:25:05.01707]: init.go:266] Waiting for the management cluster to get ready for move...
    ℹ [1217 10:25:05.01976]: clusterclient.go:1105] Waiting for resource tce-mgmt-cluster of type *v1alpha3.Cluster to be up and running
    ℹ [1217 10:25:05.05951]: clusterclient.go:1139] Waiting for resources type *v1alpha3.MachineDeploymentList to be up and running
    ℹ [1217 10:25:05.06443]: clusterclient.go:1139] Waiting for resources type *v1alpha3.MachineList to be up and running
    ℹ [1217 10:25:05.07025]: init.go:271] Waiting for addons installation...
    ℹ [1217 10:25:05.08311]: clusterclient.go:1139] Waiting for resources type *v1alpha3.ClusterResourceSetList to be up and running
    ℹ [1217 10:25:05.09952]: clusterclient.go:1105] Waiting for resource antrea-controller of type *v1.Deployment to be up and running
    ℹ [1217 10:25:05.10657]: init.go:283] Moving all Cluster API objects from bootstrap cluster to management cluster...
    ℹ [1217 10:27:06.51394]: init.go:335] Waiting for additional components to be up and running...
    ℹ [1217 10:27:06.51677]: clusterclient.go:1105] Waiting for resource tanzu-addons-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:27:06.51699]: clusterclient.go:1105] Waiting for resource tkr-controller-manager of type *v1.Deployment to be up and running
    ℹ [1217 10:27:06.51715]: clusterclient.go:1105] Waiting for resource kapp-controller of type *v1.Deployment to be up and running
    ℹ [1217 10:34:21.53553]: init.go:340] Waiting for packages to be up and running...
    ‼ [1217 10:34:21.60524]: upgrade_region.go:420] Waiting for package: antrea
    ‼ [1217 10:34:21.60527]: upgrade_region.go:420] Waiting for package: metrics-server
    ‼ [1217 10:34:21.60542]: upgrade_region.go:420] Waiting for package: tanzu-addons-manager
    ℹ [1217 10:34:21.60724]: clusterclient.go:1105] Waiting for resource tanzu-addons-manager of type *v1alpha1.PackageInstall to be up and running
    ℹ [1217 10:34:21.60724]: clusterclient.go:1105] Waiting for resource metrics-server of type *v1alpha1.PackageInstall to be up and running
    ℹ [1217 10:34:21.61111]: clusterclient.go:1105] Waiting for resource antrea of type *v1alpha1.PackageInstall to be up and running
    ℹ [1217 10:35:11.63123]: upgrade_region.go:427] Successfully reconciled package: tanzu-addons-manager
    ℹ [1217 10:35:21.62813]: upgrade_region.go:427] Successfully reconciled package: metrics-server
    ℹ [1217 10:35:21.62813]: upgrade_region.go:427] Successfully reconciled package: antrea
    ℹ [1217 10:35:21.62826]: init.go:345] Context set for management cluster tce-mgmt-cluster as 'tce-mgmt-cluster-admin@tce-mgmt-cluster'.
    ℹ [1217 10:35:21.64812]: client.go:177] Deleting kind cluster: tkg-kind-c6uaij5b5lrta6f31s40
    ℹ [1217 10:35:23.70245]: init.go:331] Management cluster created!
    ℹ [1217 10:35:23.70253]: init.go:332] You can now create your first workload cluster by running the following:
    ℹ [1217 10:35:23.70258]: init.go:333] tanzu cluster create [name] -f [file]
    ```

- Verify if the management cluster is up and running
```
$ tanzu management-cluster get
```
- You can also use the alias `mc` for management-cluster CLI
```
$ tanzu mc get
```
- As the local installation on Docker uses KinD, you can do `docker ps` and get a list of containers that are running
```
$ docker ps
CONTAINER ID   IMAGE                                                         COMMAND                  CREATED       STATUS       PORTS                                  NAMES
597663ce2e3a   projects.registry.vmware.com/tkg/kind/node:v1.21.2_vmware.1   "/usr/local/bin/entr…"   2 hours ago   Up 2 hours                                          tce-mgmt-cluster-md-0-6fcbfbc7cd-r5ln9
10cc3f78683e   projects.registry.vmware.com/tkg/kind/node:v1.21.2_vmware.1   "/usr/local/bin/entr…"   2 hours ago   Up 2 hours   45677/tcp, 127.0.0.1:45677->6443/tcp   tce-mgmt-cluster-control-plane-rnfh8
992ac34dfbee   kindest/haproxy:v20210715-a6da3463                            "haproxy -sf 7 -W -d…"   2 hours ago   Up 2 hours   33271/tcp, 0.0.0.0:33271->6443/tcp     tce-mgmt-cluster-lb

```

- At this point, your management cluster is up and running and its now time to connect it to your kubectl CLI.

## Connect to the Management Cluster using Kubectl

- Use the `tanzu mc` CLI to get the kubeconfig for the management cluster. Replace `tce-mgmt-cluster` with your cluster name.
```
$ tanzu mc kubeconfig get tce-mgmt-cluster --admin
```
outputs:
```
Credentials of cluster 'tce-mgmt-cluster' have been saved 
You can now access the cluster by running 'kubectl config use-context tce-mgmt-cluster-admin@tce-mgmt-cluster'
```
- Run the command in the output to connect kubectl with the management cluster
```
$ kubectl config use-context tce-mgmt-cluster-admin@tce-mgmt-cluster
```
outputs
```
Switched to context "tce-mgmt-cluster-admin@tce-mgmt-cluster".
```

??? info "Sample Cluster Config of the Tanzu Management cluster"
    This guy can be re-used to create workload clusters or managed clusters.
    ```
    CLUSTER_CIDR: 100.96.0.0/11
    CLUSTER_NAME: tce-mgmt-cluster
    ENABLE_MHC: "false"
    IDENTITY_MANAGEMENT_TYPE: none
    INFRASTRUCTURE_PROVIDER: docker
    LDAP_BIND_DN: ""
    LDAP_BIND_PASSWORD: ""
    LDAP_GROUP_SEARCH_BASE_DN: ""
    LDAP_GROUP_SEARCH_FILTER: ""
    LDAP_GROUP_SEARCH_GROUP_ATTRIBUTE: ""
    LDAP_GROUP_SEARCH_NAME_ATTRIBUTE: cn
    LDAP_GROUP_SEARCH_USER_ATTRIBUTE: DN
    LDAP_HOST: ""
    LDAP_ROOT_CA_DATA_B64: ""
    LDAP_USER_SEARCH_BASE_DN: ""
    LDAP_USER_SEARCH_FILTER: ""
    LDAP_USER_SEARCH_NAME_ATTRIBUTE: ""
    LDAP_USER_SEARCH_USERNAME: userPrincipalName
    OIDC_IDENTITY_PROVIDER_CLIENT_ID: ""
    OIDC_IDENTITY_PROVIDER_CLIENT_SECRET: ""
    OIDC_IDENTITY_PROVIDER_GROUPS_CLAIM: ""
    OIDC_IDENTITY_PROVIDER_ISSUER_URL: ""
    OIDC_IDENTITY_PROVIDER_NAME: ""
    OIDC_IDENTITY_PROVIDER_SCOPES: ""
    OIDC_IDENTITY_PROVIDER_USERNAME_CLAIM: ""
    OS_ARCH: ""
    OS_NAME: ""
    OS_VERSION: ""
    SERVICE_CIDR: 100.64.0.0/13
    TKG_HTTP_PROXY_ENABLED: "false"
    ```


- Run `kubectl get all` and you should see your kubernetes management cluster.

## Create Tanzu managed/workload cluster

- We start by login into our management-cluster of choice. we can use the one we just created. you can do that by `tanzu login`

```
$ tanzu login
```
outputs
```
? Select a server tce-mgmt-cluster    ()
✔  successfully logged in to management cluster using the kubeconfig tce-mgmt-cluster
```

- Find and copy the yaml file for your management-cluster. in my case, it was under `~/.config/tanzu/tkg/clusterconfigs/`.
- Update the file as needed for creating a workload cluster.
- Use the updated file to create a workload cluster.


tanzu config server list
tanzu config server delete tce-mgmt-cluster


[Continue Point 17](https://tanzucommunityedition.io/docs/latest/getting-started/)