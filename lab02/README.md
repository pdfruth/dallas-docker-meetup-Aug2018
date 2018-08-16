
## Containerize an existing web application

In this section we'll take an exising web application, *build* the "Docker container image" of it, deploy/*run* the "Docker container" and then *Stop* the "Docker container".

Frist, create a new directory to work from 
```
$ mkdir dallasmeetup
$ cd dallasmeetup
```

1. In the *dallasmeetup* directory, create webapp.js file using your preferred editor (nano, vi, etc.) and add the following code:
```
  Need the "web app" artifacts from Dave.  Below is an example of the server.js app that Richard created.
  
  var http = require('http');

  var handleRequest = function(request, response) {
  console.log('Received request for URL: ' + request.url);
  response.writeHead(200);
  response.end('Hello World!');
  };
  var www = http.createServer(handleRequest);
  www.listen(8080);
```

2. In the *dallasmeetup* directory, create a file named **Dockerfile** (it doesn't need an extension) and enter the following code using your preferred editor (nano, vi, etc.):

```
  FROM <to be provided by Dave>
  EXPOSE 8080
  COPY <to be provided by Dave>
  CMD <to be provided by Dave>
```

3. **Build** the "Docker Container image" (*docker build*) based on the **Dockerfile** you just created, name it "mynode" and tag it with "v1.0" in the current directory (* .*) you are in (*dallasmeetup*).
```
$ docker build -t mynode:v1.0 .
```

4. **Run** the "Docker Container image" (*docker run*) to deploy the container, call it "mynode-sample".  The *docker run* command first creates a writeable container layer over the specified image and then starts it using the specified command.  Remember that "Docker Container images" are just files that become containers at runtime.

```
$ docker run --rm -d -p 8080:8080 --name mynode-sample  mynode:v1.0
```

  Now, for a quick test of the container running locally on your machine, in your browser, access http://localhost:8080.  

5. **Stop** the locally running container

```  
$ docker stop mynode-sample
```


---
