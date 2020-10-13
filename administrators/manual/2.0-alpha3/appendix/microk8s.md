---
layout: page
title: Using Microk8s
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

## Overview

This document will provide instructions to using Microk8s and Kubernetes commandline to access your cluster.

## Using Microk8s
Typing microk8s will give a list of all commands:

```bash
  microk8s --help
```

```text
Available subcommands are:
	add-node
	cilium
	config
	ctr
	dashboard-proxy
	disable
	enable
	helm
	helm3
	istioctl
	join
	juju
	kubectl
	leave
	linkerd
	refresh-certs
	remove-node
	reset
	start
	status
	stop
	inspect
```

To get more details about a command:

```bash
  microk8s <command> --help
```

### Getting the Status
To check the status of your cluster and which addons are enabled.

```bash
  microk8s status
```

```text
	microk8s is running
	addons:
	dashboard: enabled
	dns: enabled
	metrics-server: enabled
	ambassador: disabled
	cilium: disabled
	fluentd: disabled
	gpu: disabled
	helm: disabled
	helm3: disabled
	host-access: disabled
	ingress: disabled
	istio: disabled
	jaeger: disabled
	knative: disabled
	kubeflow: disabled
	linkerd: disabled
	metallb: disabled
	multus: disabled
	prometheus: disabled
	rbac: disabled
	registry: disabled
	storage: disabled
```
### Starting and Stopping
MicroK8s will continue running until you decide to stop it. You can stop top MicroK8s and its services by typing the command:

```bash
  microk8s stop
```

You can restart by typing:

```bash
  microk8s start
```

### Accessing the dashboard locally
MicroK8s provides access to the standard kubernetes dashboard.  You can enable the dashboard and proxy to it on the local system.

```bash
  microk8s enable dashboard
  microk8s kubectl proxy &
```

The dashboard is available at the following URL:

```text
http://127.0.0.1:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/
```

## Using Kubernetes
MicroK8s bundles its own version of kubectl for accessing Kubernetes. Use it to run commands to monitor and control your Kubernetes. Kubectl commands are prefixed by microk8s. 

### To get a list of commands:

```bash
  microk8s kubectl
```

```text
	kubectl controls the Kubernetes cluster manager.
	
	 Find more information at: https://kubernetes.io/docs/reference/kubectl/overview/
	
	Basic Commands (Beginner):
	  create        Create a resource from a file or from stdin.
	  expose        Take a replication controller, service, deployment or pod and expose it as a new Kubernetes Service
	  run           Run a particular image on the cluster
	  set           Set specific features on objects
	
	Basic Commands (Intermediate):
	  explain       Documentation of resources
	  get           Display one or many resources
	  edit          Edit a resource on the server
	  delete        Delete resources by filenames, stdin, resources and names, or by resources and label selector
	
	Deploy Commands:
	  rollout       Manage the rollout of a resource
	  scale         Set a new size for a Deployment, ReplicaSet or Replication Controller
	  autoscale     Auto-scale a Deployment, ReplicaSet, or ReplicationController
	
	Cluster Management Commands:
	  certificate   Modify certificate resources.
	  cluster-info  Display cluster info
	  top           Display Resource (CPU/Memory/Storage) usage.
	  cordon        Mark node as unschedulable
	  uncordon      Mark node as schedulable
	  drain         Drain node in preparation for maintenance
	  taint         Update the taints on one or more nodes
	
	Troubleshooting and Debugging Commands:
	  describe      Show details of a specific resource or group of resources
	  logs          Print the logs for a container in a pod
	  attach        Attach to a running container
	  exec          Execute a command in a container
	  port-forward  Forward one or more local ports to a pod
	  proxy         Run a proxy to the Kubernetes API server
	  cp            Copy files and directories to and from containers.
	  auth          Inspect authorization
	
	Advanced Commands:
	  diff          Diff live version against would-be applied version
	  apply         Apply a configuration to a resource by filename or stdin
	  patch         Update field(s) of a resource using strategic merge patch
	  replace       Replace a resource by filename or stdin
	  wait          Experimental: Wait for a specific condition on one or many resources.
	  convert       Convert config files between different API versions
	  kustomize     Build a kustomization target from a directory or a remote url.
	
	Settings Commands:
	  label         Update the labels on a resource
	  annotate      Update the annotations on a resource
	  completion    Output shell completion code for the specified shell (bash or zsh)
	
	Other Commands:
	  alpha         Commands for features in alpha
	  api-resources Print the supported API resources on the server
	  api-versions  Print the supported API versions on the server, in the form of "group/version"
	  config        Modify kubeconfig files
	  plugin        Provides utilities for interacting with plugins.
	  version       Print the client and server version information
	
	Usage:
	  kubectl [flags] [options]
	
	Use "kubectl <command> --help" for more information about a given command.
	Use "kubectl options" for a list of global command-line options (applies to all commands).
```
### To view your node:

```bash
  microk8s kubectl get nodes
```

### To view the cluster info:

```bash
  microk8s kubectl cluster-info
```

### To view everything currently running in the cluster


```bash
  microk8s kubectl get all --all-namespaces
```

### To view running services in the default namespace:

```bash
  microk8s kubectl get services
```
* use `--all-namespaces` for all services in all namespaces
* use `-n kube-system` for the kubernetes system
* use `-n lockss` for lockss specific services

### To view the logs of a pod:

```bash
microk8s kubectl get pods 
microk8s kkubectl logs <podname>
```

### To describe a running pod:

```bash
microk8s kubectl get pods 
microk8s kkubectl describe <podname>
```


### For details about a specfic command

```bash
  microk8s kubectl <command> --help
```
