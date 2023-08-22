---
title: "How to set up a Kubernetes (K8S) Cluster on the fly?"
seoTitle: "How to set up a Kubernetes (K8S) Cluster using kubeadm"
datePublished: Mon Aug 21 2023 11:10:33 GMT+0000 (Coordinated Universal Time)
cuid: cllks04oz000a0alggmi7dy8b
slug: how-to-set-up-a-kubernetes-k8s-cluster-on-the-fly
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692610100757/e3aef2d2-5aa8-4cd6-a2e7-53ab63467709.gif
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692616213037/24348d37-0fdd-42fd-9e86-f93b578f9b0d.gif
tags: kubernetes, developer, devops, 90daysofdevops, trainwithshubham

---

### Pre-requisites:

* Ubuntu OS (Xenial or later)
    
* sudo privileges
    
* Internet access
    
* t2.medium instance type or higher
    

### What you will learn in this article:

With the below image, you will get a better idea about what you will learn in this article  

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692615901530/af4a462c-7e5a-4a2e-b282-76c45a70e4f3.gif align="center")

For Kubernetes setup using Kubeadm, we will need **at least two machines.**

Here, we will launch two ec2 instances from Amazon AWS.

## For both ec2 instances:

Now **in both instances** follow the below 3 steps

**Step 1)** Install , start, enable docker

**Step 2)** Download Kubernetes binaries

**Step 3)** Install kubeadm

```bash
sudo su
apt update -y
apt install docker.io -y

systemctl start docker
systemctl enable docker

curl -fsSL "https://packages.cloud.google.com/apt/doc/apt-key.gpg" | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/kubernetes-archive-keyring.gpg
echo 'deb https://packages.cloud.google.com/apt kubernetes-xenial main' > /etc/apt/sources.list.d/kubernetes.list

apt update -y
apt install kubeadm=1.20.0-00
```

## For 1st EC2 instance:

Now , **one** of the two ec2 machine where we wants to create master node follow below steps:

**Step 1 )** Initialize the Kubernetes master node.

```bash
sudo su
apt install kubectl=1.20.0-00
kubeadm init
```

After successfully running, your Kubernetes control plane will be initialized successfully and the master node gets created.  
also, we have installed "**kubectl**" a command line utility and this will allows us to interact with Kubernetes cluster.

Here, once we enter "**kubeadm init**" it will immediately **create a cluster** and **setup master node** with all required service components **i.e. api server, scheduler, controller manager, etcd.**

**Step 2)** Set up local kubeconfig (both for root user and normal user):

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Here, we are copying the config file and setting ownership of file to our user. so that user can access that file without any access issues.

**Step 3)** Apply one CNI network

```bash
kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
```

here, we have created a weave network as CNI for our cluster. So, our master sevices , nodes can communicate with this network.

**Step 4)** Generate a token for worker nodes to join:

```bash
kubeadm token create --print-join-command
```

With this command , we can create and print a token which will be helpful while joining nodes on our cluster.

**Step 5)** On this 1st ec2 **expose port 6443** in the Security group so that the worker node can connect with the cluster when we join in the next step.

## For 2nd ec2 instance:

**Step 1)** Run the following commands on the worker node

```bash
sudo su
kubeadm reset pre-flight checks
```

**Step 2)** Paste the join command you got from the master node (step 4) and append `--v=5` at the end

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692612549132/7a137883-acbe-4611-97fa-bc9a16e6bd49.png align="center")

After succesful join-&gt;

![image](https://user-images.githubusercontent.com/40052830/261848460-c530b65a-4afd-4b1d-9748-421c216d64cd.png align="left")

In this way, our setup for kubernetes cluster is ready with master node and one worker node.  
Now, we can access pods inside worker node by hitting below command in 1st ec2 machine where master node is available and test our cluster connection.

```bash
kubectl get nodes
```

## Test a "Demo Pod":

If you want to test a demo pod, you can use the following command on 1st ec2 machine:  
Here, i am taking simple image for example. But, you can use any real time project service image.

```bash
kubectl run hello-world-pod --image=busybox --restart=Never --command -- sh -c "echo 'Hello, World' && sleep 3600"
```

![image](https://user-images.githubusercontent.com/40052830/261848566-bace1884-bbba-4e2f-8fb2-83bbba819d08.png align="left")

Hope this article helped you in your learning.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692613645161/7cd29de8-5c9c-4a24-aca1-cf012d838c16.jpeg align="center")

### Happy Learning