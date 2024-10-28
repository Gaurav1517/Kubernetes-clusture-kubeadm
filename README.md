# Kubernetes-clusture-kubeadm
Create kubernetes v1.29 clusture using kubeadm in centos-8 

# Kubernetes Installation Steps

This document outlines the steps to install and configure Kubernetes on a Linux system, including firewall configurations and the installation of required components.

## Table of Contents

1. [Disable Firewall or Allow Ports](#disable-firewall-or-allow-ports)
2. [Disable Swap](#disable-swap)
3. [Load Kernel Modules](#load-kernel-modules)
4. [Install and Configure Containerd](#install-and-configure-containerd)
5. [Install CRI-O](#install-cri-o)
6. [Set Up Kubernetes YUM Repository](#set-up-kubernetes-yum-repository)
7. [Install Kubelet, Kubeadm, and Kubectl](#install-kubelet-kubeadm-and-kubectl)
8. [Initialize Kubernetes Control Plane](#initialize-kubernetes-control-plane)
9. [Install Calico Network Plugin](#install-calico-network-plugin)
10. [Join Worker Node to the Cluster](#join-worker-node-to-the-cluster)
11. [Kubernetes Cheat Sheet](#kubernetes-cheat-sheet)

## Disable Firewall or Allow Ports

You can either disable the firewall or allow specific ports for Kubernetes.

### Disable Firewall
```bash
systemctl stop firewalld.service
systemctl disable firewalld.service
systemctl status firewalld.service
```
## Allow Firewall Ports on Master Node

To open specific ports, run the following commands:
```bash
# Open port 6443 for the Kubernetes API server
sudo firewall-cmd --zone=public --add-port=6443/tcp --permanent

# Open ports 2379-2380 for etcd server client API
sudo firewall-cmd --zone=public --add-port=2379-2380/tcp --permanent

# Open port 10250 for Kubelet API
sudo firewall-cmd --zone=public --add-port=10250/tcp --permanent

# Open port 10259 for kube-scheduler
sudo firewall-cmd --zone=public --add-port=10259/tcp --permanent

# Open port 10257 for other Kubernetes services
sudo firewall-cmd --zone=public --add-port=10257/tcp --permanent
```
## To add multiple ports in a single command:
```bash
sudo firewall-cmd --zone=public --add-port=6443/tcp,2379-2380/tcp,10250/tcp,10259/tcp,10257/tcp --permanent
```
## Reload Firewall
```bash
sudo firewall-cmd --reload
```
## Check Firewall Ports
```bash
sudo firewall-cmd --zone=public --list-ports
```

## Allow Ports on Worker Node
To allow additional ports on the worker node:
```bash

# Open port 10250 for Kubelet API
sudo firewall-cmd --zone=public --add-port=10250/tcp --permanent

# Open port 10256 for kube-proxy
sudo firewall-cmd --zone=public --add-port=10256/tcp --permanent

# Open port range 30000-32767 for NodePort services
sudo firewall-cmd --zone=public --add-port=30000-32767/tcp --permanent
```

## Or, add these additional ports in a single command:

```bash
sudo firewall-cmd --zone=public --add-port=10250/tcp,10256/tcp,30000-32767/tcp --permanent
```

## Reload Firewall on Worker Node

```bash
sudo firewall-cmd --reload
```

## Check Firewall Ports on Worker Node

```bash
sudo firewall-cmd --zone=public --list-ports
```

## Disable Swap
Disable swap if not on a cloud instance:

```bash
sudo swapoff -a
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
```



