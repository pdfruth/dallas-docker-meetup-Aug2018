
## Containerize an existing web application

In this section we'll take an exising web application and containerize it in a Docker container.

Create a new directory to work from 
```
$ mkdir dallasmeetup
$ cd dallasmeetup
```

1. In the *dallasmeetup* directory, create a file named **Dockerfile** (it doesn't need an extension) and enter the following code using your preferred editor (nano, vi, etc.):

```
  FROM node: <to be provided>
  EXPOSE 8080
  COPY <to be provided>
  CMD <to be provided>
```

2. **Build** the "Docker Container image" (*docker build*) based on the **Dockerfile** you just created, name it "mynode" and tag it with "v1.0" in the current directory (* .*) you are in (*dallasmeetup*).
```
$ docker build -t mynode:v1.0 .
```

3. **Run** the "Docker Container image" (*docker run*) to deploy the container, call it "mynode-sample".  The *docker run* command first creates a writeable container layer over the specified image and then starts it using the specified command.  Remember that "Docker Container images" are just files that become containers at runtime.

```
$ docker run --rm -d -p 8080:8080 --name mynode-sample  mynode:v1.0
```

  Now, for a quick test of the container running locally on your machine, in your browser, access http://localhost:8080.  

4. Stop the locally running container

```  
$ docker stop mynode-sample
```


---
