**In this section**, you will learn how to upload a "Docker container image" to Dockerhub and deploy it to our cluster. 

Development processes such as these are typically sped up with enhancements such as automated DevOps processes, however this is a helpful to get a fundamental look at how some of the underlying parts of the process work.

Back in [lab 02](lab02/README.md) we built a "Docker container image" of the web app and ran it in the Docker runtime on our local machines (remember that?). Well now, we'll move a copy of that "Docker container image" to our **Dockerhub** account so it's available to run in our IBM Cloud Private (ICP) cluster.

First lets "tag" our "Docker container image". 
```

$ docker tag mynode:v1.0 ehamamcy/mynode:v1.0
$ docker images

```

"Tagging" the "Docker container image" tells it where to go when we "push" to a remote repository. By default it will upload to the repository at *hub.docker.com* (unless syou specify otherwise). 

Now we'll upload the image with *docker push*:
```
$ docker push ehamamcy/mynode:v1.0
```

From here, if you check your browser and look at the list of available "tags" in the repositoy we created, you should see your new image!

---

From here, we can *run* the "Docker container image" on our ICP Kubernetes cluster.

```
$ kubectl run hello-node --image=ehamamcy/mynode:v1.0 --port=8080 --namespace=user99-ns
deployment "hello-node" created

$ kubectl get deployment --namespace=user99-ns
NAME         DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
hello-node   1         1         1            1           29s
$
$ kubectl get pods --namespace=user99-ns
NAME                         READY     STATUS    RESTARTS   AGE
hello-node-77c96d485-qstmk   1/1       Running   0          3m

```

With the Docker container running, we'll need to expose the applications port before we can access to application.


```
$ kubectl expose deployment hello-node --type=NodePort  --namespace=user99-ns
service "hello-node" exposed
$ kubectl get services
NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
hello-node   NodePort    10.97.250.220   <none>        8080:32644/TCP   4s
kubernetes   ClusterIP   10.96.0.1       <none>        443/TCP          5h

```

Now that the application is accessible via an external port, we're able to gain access to the services with the *curl* command

```  
$ kubectl get service --namespace=user99-ns
NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
hello-node   NodePort    10.97.250.220   <none>        8080:32644/TCP   1m
kubernetes   ClusterIP   10.96.0.1       <none>        443/TCP          5h


```
Then we can assemble the URL as http:// + [icp master ip] + ":" + [port assigned by the service].
If the IP address for the Master node of our ICP cluster is 192.168.99.100 then we should use http://192.168.99.100:30839 to access our new service.


We've built and run our first container on Kubernetes!

---
