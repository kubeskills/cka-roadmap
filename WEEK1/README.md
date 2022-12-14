# WEEK 1

## Installing a Cluster using Kubeadm

### This is week's content is within the cluster architecture, installation & configuration section of the exam curriculum
- [Exam Curriculum](https://github.com/cncf/curriculum/blob/master/CKA_Curriculum_v1.24.pdf)

We'll dive into how a cluster is created in order to better understand all the moving parts of a Kubernetes
cluster and the cluster bootstrap process.

---
## Exercises

1. Create a script that installs Kubernetes on a VM (any VM will do). Use the example [here](https://github.com/kubeskills/cka-roadmap/blob/main/WEEK1/example-install-k8s.sh) as a template for your script, where the script will install version 1.24.0 of kubeadm, kubelet, and kubectl and also preps the flannel CNI for being installed. 
2. Create an "init script" that will only run on the control plane server in order to bootstrap or initialize the cluster