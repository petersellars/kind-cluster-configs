# Basic Cluster Operations
This page provides information on basic kind cluster creation.

To create a cluster with the default cluster context name use this command:
```
$ kind create cluster
```

To create a cluster with a different cluster context name use the `--name flag`:
```
$ kind create cluster --name kind2
```

You can also specify a period of time for the command to block until the control plane reaches a steady state using the `--wait` flag:
```
$ kind create cluster --name kind2 --wait 30s
```

To delete a cluster use the `delete cluster` command:
```
kind delete cluster --name kind
```

## Loading an Image into your kind Cluster
To make an image available for use in the kind cluster you need to load an image into the cluster.

```
$ kind load docker-image hello-world:latest
```
_NOTE_: Don't use the `:latest` tag in real use cases as this would result in the image never being updated.

You can ensure it is loaded by getting a list of images present on a cluster node:
```
$ docker exec -it <node-name> crictl images
```