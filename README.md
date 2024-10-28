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

