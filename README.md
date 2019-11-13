# Kubernetes Cluster setup with Kubeadm, Vagrant and Ansible

### Overview
This repo helps setup a multi node kubernetes cluster with kubeadm, vagrant and ansible for development and demo purposes. 

Kubernetes Setup -

* 1 Master node
* 2 Worker nodes
* CNI - Flannel


### Pre-Requisites

* Vagrant (2.2.x)
	* vagrant-hostsupdater plugin ( `vagrant plugin install vagrant-hostsupdater` )

* Virtualbox (6.x)

* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) 


### Steps

1. Clone repo and change directory to kubernetes-cluster-vagrant folder

`cd kubernetes-cluster-vagrant`

2. Setup cluster with executing vagrant command. This command will download ubuntu base image.  

`vagrant up`


3. Vagrant uses ansible provisioner to run roles required for master and worker nodes. once setup is complete, you will notice `kubeconfig` is copied in your working folder.

4. execute `export KUBECONFIG=kubeconfig` on terminal

5. verify status of cluster

`kubectl get nodes`
`kubectl cluster-info`

6. To Destroy, run `vagrant destroy -f`

**NOTE**
This demostration is tested on macOS. 





