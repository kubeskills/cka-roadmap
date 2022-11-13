# WEEK 8

## Working with storage in Kubernetes

### This is week's content is within the storage section of the exam curriculum
- [Exam Curriculum](https://github.com/cncf/curriculum/blob/master/CKA_Curriculum_v1.24.pdf)

We'll discover working with persistent volumes and persistent volume claims when attached to pods, either within a deployment or standalone. We'll also discuss the need for storage classes and volumes that need additional access parameters.

### RESOURCES

- [VIDEO: Volumes Explained](https://youtu.be/0swOh5C3OVM)
- [VIDEO: Persistent Volumes Exercises](https://youtu.be/ZxC6FwEc9WQ)
- [VIDEO: PV in Cloud Storage](https://youtu.be/pumX2Ds5L0c)
- [EXERCISE: PV with MySQL](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/)
- [TUTORIAL: Persistent Volumes](https://www.containiq.com/post/kubernetes-persistent-volumes)
- [TUTORIAL: Volumes](https://redhat-scholars.github.io/kubernetes-tutorial/kubernetes-tutorial/volumes-persistentvolumes.html)

### CHALLENGES

1. Configure a hostpath persistent volume named `vol02833` with a size of `10GB` of local storage from the worker node host “node01” (node name will be different if not using killercoda). The directory on the host should be “/mnt/data.”
2. Create a persistent volume claim named `claim-02833` that will reserve `9GB` of storage from the volume `vol02833`. 
3. Mount the volume to a pod within a deployment named `frontend0113`. The mount path within the container should be `/usr/share/nginx/html`.