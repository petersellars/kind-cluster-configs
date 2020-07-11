# kind Cluster Configurations
[kind](https://kind.sigs.k8s.io/) is a tool for running local Kubernetes clusters using Docker container "nodes". kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

I use this repository to store useful kind configurations.

## Pre-requisites
To use the configurations in this repository ensure you have the following installed:

* [go](https://golang.org/) (1.14+)
* [Docker](https://www.docker.com/)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

To set up auto-completion for commands on the CLI on bash you can run the `kind completion bash` command with bash completions

```
sudo apt | dnf | pacman install bash-completion
kind completion bash | sudo tee /etc/bash_completion.d/kind
source ~/.bashrc
```

## Useful kind Cluster Commands
These commands can help you inspect your cluster.

To list your kind clusters use the `get clusters` command
```
$ kind get clusters
kind
kind-2
```

To list your kind cluster nodes use the `get nodes` command
```
$ kind get nodes
kind-control-plane
```

To interact with a specific cluster you need to specify the cluster name. You can get basic cluster informationusing the `kubectl cluster-info` command

```
$ kubectl cluster-info --context kind-kind
```

By default, the cluster access configuration is stored in `$HOME/.kube/config`. You can inspect this file

```
$ less $HOME/.kube/config
```
Or
```
$ kind get kubeconfig
```

See `kind create cluster --help` for more info on the kubeconfig path configuration and more.

## In-Depth kind Cluster Commands
These commands are for getting more in-depth information about your kind cluster.

To get a list of Docker images present on a cluster node you can use the `docker exec` command

```
$ docker exec -it kind-control-plane crictl images
IMAGE                                                  TAG                  IMAGE ID            SIZE
docker.io/kindest/kindnetd                             v20200619-15f5b3ab   ddb3bf692bfe2       120MB
docker.io/rancher/local-path-provisioner               v0.0.12              db10073a6f829       42MB
k8s.gcr.io/coredns                                     1.6.7                67da37a9a360e       43.9MB
k8s.gcr.io/etcd                                        3.4.3-0              303ce5db0e90d       290MB
k8s.gcr.io/kube-apiserver                              v1.18.4              006ea3edd9283       147MB
k8s.gcr.io/kube-controller-manager                     v1.18.4              9e1588c3bb096       133MB
k8s.gcr.io/kube-proxy                                  v1.18.4              d51177d3cef3a       133MB
k8s.gcr.io/kube-scheduler                              v1.18.4              09410b9bd5e91       113MB
k8s.gcr.io/pause                                       3.2                  80d28bedfe5de       686kB
us.gcr.io/k8s-artifacts-prod/build-image/debian-base   v2.1.0               c7c6c86897b63       53.9MB
```

In the eample above the node inspected is the `kind-control-plane`. You should update the command with the name of the nod you wish to inspect.