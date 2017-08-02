# Kubernetes Offline

Offline installation package for kubernetes.

## Introduction

This project is modified from [k8s-deploy](https://github.com/xiaoping378/k8s-deploy), it provides offline installation solution for Kubernetes 1.5 & 1.6. It is useful to deploy K8S to OFFLINE production environment.

The offline installation package will install:

* Docker (1.12.6)
* All the kubernetes components
* Kubernetes dashboard. The default node port for dashboard is: 31234

## Requirement & Limitation

* These installation packages are __ONLY FOR CentOS__.
* All these installation packages are installed & verified by: __CentOS Linux release 7.3.1611 (Core)__
* Right now, all these offline packages only install K8S master for __SINGLE__ instance, K8S master HA is __NOT__ supported yet.

## Install offline package for K8S 1.5

### Prepare the dispatch server
1. Downlaod packages from 百度网盘:
   URL: [https://pan.baidu.com/s/1mikM3Ao](https://pan.baidu.com/s/1mikM3Ao)
   Code: bvj5
2. Copy it to the production server
3. Go to the offline package directory, host it with a simple HTTP server:

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

## Install offline package for K8S 1.6

Downlaod packages from 百度网盘:
URL: [https://pan.baidu.com/s/1jIHu7H0](https://pan.baidu.com/s/1jIHu7H0)  Code: 61b4

Steps are the same with K8S 1.5, but you need to notice the differences:

* Remember to reload the shell after master installation is completed:  ```source ~/.bashrc```
* To install K8S node, don't forget the port: ```6443```

   ```bash
   curl -L http://192.168.0.10:8000/install.sh |  bash -s join --token=f8c407.9aa4bb840dfe2da0 192.168.0.10:6443
   ```




