#### 1. Create a deployment named “apache” that uses the image httpd:2.4.54 and contains three pod replicas. 

##### Commands

```bash
# create apache deployment with 3 replicas
k create deploy apache --image=httpd:2.4.54 --replicas=3

# check the deployments
k get deploy

# check the replicasets
k get rs

# check the pods
k get po -o wide

```

##### Commands Output

```bash
# create apache deployment with 3 replicas
controlplane $ k create deploy apache --image=httpd:2.4.54 --replicas=3
deployment.apps/apache created

# check the deployments
controlplane $ k get deploy
NAME     READY   UP-TO-DATE   AVAILABLE   AGE
apache   3/3     3            3           61s

# check the replicasets
controlplane $ k get rs
NAME                DESIRED   CURRENT   READY   AGE
apache-74f79bcc68   3         3         3       50s


# check the pods.
controlplane $ k get po -o wide
NAME                      READY   STATUS    RESTARTS   AGE   IP            NODE           NOMINATED NODE   READINESS GATES
apache-74f79bcc68-bc2fh   1/1     Running   0          26s   192.168.1.5   node01         <none>           <none>
apache-74f79bcc68-m4xsh   1/1     Running   0          26s   192.168.1.4   node01         <none>           <none>
apache-74f79bcc68-pcjkw   1/1     Running   0          26s   192.168.0.7   controlplane   <none>           <none>

```


#### 2. After the deployment has been created, scale the deployment to five replicas

##### Commands

```bash
# scale deployment to 5 replicas
k scale deploy apache --replicas=5

# check the deployments
k get deploy

# check the replicasets
k get rs

# check the pods
k get po -o wide
```

##### Commands Output

```bash
# scale deployment to 5 replicas
controlplane $ k scale deploy apache --replicas=5
deployment.apps/apache scaled

# check the deployments
controlplane $ k get deploy
NAME     READY   UP-TO-DATE   AVAILABLE   AGE
apache   5/5     5            5           8m34s

# check the replicasets
controlplane $ k get rs
NAME                DESIRED   CURRENT   READY   AGE
apache-74f79bcc68   5         5         5       8m34s

# check the pods
controlplane $ k get po -o wide
NAME                      READY   STATUS    RESTARTS   AGE     IP            NODE           NOMINATED NODE   READINESS GATES
apache-74f79bcc68-bc2fh   1/1     Running   0          8m34s   192.168.1.5   node01         <none>           <none>
apache-74f79bcc68-fn68h   1/1     Running   0          3m11s   192.168.1.6   node01         <none>           <none>
apache-74f79bcc68-m4xsh   1/1     Running   0          8m34s   192.168.1.4   node01         <none>           <none>
apache-74f79bcc68-pcjkw   1/1     Running   0          8m34s   192.168.0.7   controlplane   <none>           <none>
apache-74f79bcc68-sq9hd   1/1     Running   0          3m11s   192.168.0.8   controlplane   <none>           <none>
```


#### 3. Change the image for the "apache" deployment to httpd:alpine

##### Commands

```bash
# change the image to httpd:alpine
k set image deploy apache httpd=httpd:alpine
```

##### Commands Output

```bash
# change the image to httpd:alpine
controlplane $ k set image deploy apache httpd=httpd:alpine
deployment.apps/apache image updated
```


#### 4. Look at the rollout history, then go back to the previous rollout (roll back) 

##### Commands

```bash
# Look at the rollout history
k rollout history deploy apache

# rollback
k rollout undo deploy apache

# check replicasets
k get rs

# check pods
k get po -o wide

k describe po apache-*-* | grep -i image:
```

##### Commands Output

```bash
# Look at the rollout history
controlplane $ k rollout history deploy apache
deployment.apps/apache 
REVISION  CHANGE-CAUSE
1         <none>
2         <none>

# rollback
controlplane $ k rollout undo deploy apache 
deployment.apps/apache rolled back

# check replicasets
controlplane $ k get rs
NAME                DESIRED   CURRENT   READY   AGE
apache-698b8cccbd   0         0         0       7m36s
apache-74f79bcc68   5         5         5       19m

# check pods
controlplane $ k get po -o wide
NAME                      READY   STATUS    RESTARTS   AGE   IP             NODE           NOMINATED NODE   READINESS GATES
apache-74f79bcc68-6swvn   1/1     Running   0          51s   192.168.1.11   node01         <none>           <none>
apache-74f79bcc68-7wxc6   1/1     Running   0          52s   192.168.1.10   node01         <none>           <none>
apache-74f79bcc68-h4dk2   1/1     Running   0          50s   192.168.1.12   node01         <none>           <none>
apache-74f79bcc68-jkwq8   1/1     Running   0          52s   192.168.0.11   controlplane   <none>           <none>
apache-74f79bcc68-n4gzx   1/1     Running   0          50s   192.168.0.12   controlplane   <none>           <none>

# check one of the pods and see that its image is set back to httpd:2.4.54
controlplane $ k describe po apache-74f79bcc68-6swvn | grep -i image:
    Image:          httpd:2.4.54
```

