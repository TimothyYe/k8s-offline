# Kubernetes Offline

Offline installer for kubernetes.

## Introduction

This project is modified from [k8s-deploy](https://github.com/xiaoping378/k8s-deploy), it provides offline installation solution for kubernetes. It is useful for deploying K8S to __OFFLINE__ production environment.

#### Supported kubernetes version:
* 1.5.1
* 1.6.2
* 1.7.2

#### The offline installer will install:

* Docker (1.12.6)
* All the kubernetes components
* Kubernetes dashboard, with default node port:```31234```

## Requirement & Limitation

* Offline installer is __ONLY FOR CentOS__.
* All the installers are installed & verified by: __CentOS Linux release 7.3.1611 (Core)__
* Right now, offline installer only installs K8S master for __SINGLE__ instance, K8S master HA is __NOT__ supported yet.

## Navigation

[Offline installer for K8S 1.5](#offline-installer-for-k8s-15)

[Offline installer for K8S 1.6](#offline-installer-for-k8s-16)

[Offline installer for K8S 1.7](#offline-installer-for-k8s-17)

## Offline installer for K8S 1.5

__Kubernetes Version: 1.5.1__

### Prepare the dispatch server
1. Downlaod installer from 百度网盘:
   URL: [https://pan.baidu.com/s/1mikM3Ao](https://pan.baidu.com/s/1mikM3Ao)
   Code: bvj5
2. Copy it to the production server
3. Go to the installer directory, host it with a simple HTTP server by Python:

```bash
[root@master k8s-deploy-1.5]# python -m SimpleHTTPServer
Serving HTTP on 0.0.0.0 port 8000 ...
```

### Install K8S master

1. Get the IP address of dispatch server, for example: 192.168.0.10
2. Install K8S master via curl:

   ```bash
   curl -L http://192.168.0.10:8000/install.sh | bash -s master
   ```
   
3. When you see that "K8S master install finished!" remember the token output like this: "  kubeadm join --token f8c407.9aa4bb840dfe2da0 192.168.0.104"

### Install K8S node

To initialize a node & join the K8S cluster is simple:

```bash
curl -L http://192.168.0.10:8000/install.sh |  bash -s join --token=f8c407.9aa4bb840dfe2da0 192.168.0.10
```

Repeat this step if you want to setup multiple K8S nodes.

### Access the kubernetes dashboard

```http://(master or node IP):31234```

## Offline installer for K8S 1.6

__Kubernetes Version: 1.6.2__

Downlaod installer from 百度网盘:
URL: [https://pan.baidu.com/s/1jIHu7H0](https://pan.baidu.com/s/1jIHu7H0)  Code: 61b4

Steps are the same with K8S 1.5, but you need to notice the differences:

* Remember to reload the shell after master installation is completed:  ```source ~/.bashrc```
* To install K8S node, don't forget the port: ```6443```

```bash
curl -L http://192.168.0.10:8000/install.sh |  bash -s join --token=f8c407.9aa4bb840dfe2da0 192.168.0.10:6443
```

## Offline installer for K8S 1.7

__Kubernetes Version: 1.7.2__

Downlaod installer from 百度网盘:
URL: [https://pan.baidu.com/s/1pLLUiSj](https://pan.baidu.com/s/1pLLUiSj)  Code: ye2k

Steps are the same with K8S 1.6.


