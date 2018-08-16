
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

3. **Build** the "Docker Container image" (*docker build*)
```
$ docker build -t mynode:v1.0 .
```

4. **Run** the "Docker Container image" (*docker run*) and test it locally.  The *docker run* command first creates a writeable container layer over the specified image and then starts it using the specified command.  Remember that "Docker Container images" become containers at runtime.

```
$ docker run --rm -d -p 8080:8080 --name mynode-sample  mynode:v1.0
```

  For a quick test of the container running locally on your machine, in your browser, access http://localhost:8080.  

5. Stop the locally running container

```  
$ docker stop mynode-sample
```


---
