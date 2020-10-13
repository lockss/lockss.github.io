---
layout: page
title: Configuring DNS
---

*This information applies to version 2.0-alpha3 of the LOCKSS system.*

After MicroK8s is up and running, adjustments need to be made to DNS processing in MicroK8s, which is handled by a MicroK8s component named CoreDNS. In this section, you will first make use of the LOCKSS Installer you downloaded from GitHub a few sections ago.

## Configuring DNS

From the `lockss-installer` directory and as the `lockss` user, run the following script:

```bash
scripts/configure-dns
```

You may be prompted for the `lockss` password for `sudo`, and under some circumstances, you may be prompted for a semicolon-separated list of IP addresses of upstream DNS servers your host machine should use.

## Example 1

Successful output from a run not requiring IP addresses of upstream DNS servers will look something like the following:

```text
Enabling DNS
Applying manifest
serviceaccount/coredns created
configmap/coredns created
deployment.apps/coredns created
service/kube-dns created
clusterrole.rbac.authorization.k8s.io/coredns created
clusterrolebinding.rbac.authorization.k8s.io/coredns created
Restarting kubelet
DNS is enabled
Updating CoreDNS ConfigMap to use /etc/resolv.conf...
configmap/coredns configured
--------------------------------------------------------------------
Successfully changed CoreDNS ConfigMap
    forward . /etc/resolv.conf
--------------------------------------------------------------------
```

## Example 2

Successful output from a run requiring IP addresses of upstream DNS servers (where the proposed default is simply accepted with the Enter key) will look something like the following:

```text
Enabling DNS
Applying manifest
serviceaccount/coredns created
configmap/coredns created
deployment.apps/coredns created
service/kube-dns created
clusterrole.rbac.authorization.k8s.io/coredns created
clusterrolebinding.rbac.authorization.k8s.io/coredns created
Restarting kubelet
DNS is enabled
The /etc/resolv.conf file in your system contains a loopback address.
CoreDNS does not allow a loopback address to be assigned to pods.
Please enter a list of ip addresses of upstream dns resolvers.
IP address(es) for dns lookup, separated by ';': [8.8.8.8;8.8.4.4] 
Updating CoreDNS ConfigMap to use  8.8.8.8 8.8.4.4...
configmap/coredns configured
--------------------------------------------------------------------
Successfully changed CoreDNS ConfigMap
    forward .  8.8.8.8 8.8.4.4
--------------------------------------------------------------------
```

## Verifying CoreDNS

If you type:

```bash
microk8s kubectl get all --all-namespaces
```

you will see output similar to the following:

```text
NAMESPACE     NAME                           READY   STATUS    RESTARTS   AGE
kube-system   pod/coredns-588fd544bf-xq8ck   1/1     Running   0          5h51m

NAMESPACE     NAME                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                  AGE
default       service/kubernetes   ClusterIP   10.152.183.1    <none>        443/TCP                  23h
kube-system   service/kube-dns     ClusterIP   10.152.183.10   <none>        53/UDP,53/TCP,9153/TCP   5h51m

NAMESPACE     NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
kube-system   deployment.apps/coredns   1/1     1            1           5h51m

NAMESPACE     NAME                                 DESIRED   CURRENT   READY   AGE
kube-system   replicaset.apps/coredns-588fd544bf   1         1         1       5h51m
```

consisting of sections for different kinds of resources: pods, services, deployments, replica sets, etc. The pod containing `coredns` in the name (here `pod/coredns-588fd544bf-xq8ck`) should be in `Running` status and display `1/1` (one of one) ready.

## Frequently Asked Questions

**Under what circumstances will IP addresses of upstream DNS servers be needed?**

On your host system, if `/etc/resolv.conf` (and `/run/systemd/resolve/resolv.conf` if your system uses `systemd-resolved`) contains `nameserver` lines for `localhost`, `::1`, `127.0.0.1`, or other loopback addresses, then `configure-dns` will prompt you for a semicolon-separated list of IP addresses of upstream DNS servers.
