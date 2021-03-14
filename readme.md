# NodeJs app Docker locally on Windows 10 Home edition


## Setup:
1. Install Docker Desktop for Windows and Enable 'Use the WSL2 based engine..'
2. Enable Kubernetes in Docker Desktop
3. Install command line tools in WSL2

## Build container and run from WSL
1. To build the container run the following 

`docker build . -t hello-docker-nodejs`


2. Above lists the container id.  Launch the container using the id

`docker run -p 3000:3000 f5ec8a4a7ce2`


3. Visit the website using browser or run curl command.


4.  Stop docker (from another window)
`docker ps`
`docker stop <container id>`


5. Prune everything... (CAUTION.. below removes everything from Docker including other projects and images).  Do it only if needed...
`docker system prune -a`


# Use Kubernetes to run above container

## Kube commands
1. Get existing pods
`kubectl get pod`   - Get information about all running pods

2. Create pod for the hello world nodejs app
`kubectl create -f kubernetes/helloworld.yml`  

Note:  `imagePullPolicy` should be set to `Never` which forces kubernetes to use local image

3. Create a service using command line for now. 
`kubectl port-forward hello-docker-node 8080:3000`

And test it by visiting localhost:8080 (curl or browser).  ^C to exit the command line afterwords

4. Expose the service
`kubectl expose pod hello-docker-node --type=NodePort --name=hello-docker-node-service`
The service is exposed.  It will chose a random port from local host to forward the traffic to above container.  Obtain the IP addres by running 
`kubectl get services`

Visit localhost:31828.  Note that the port will be different and it is obtained from the kubectl get services command.

5. Get more information about the service as follows
`kubectl describe service hello-docker-node-service`



# Important Kubectl commands

`kubectl describe pod <pod>` 

`kubectl expose pod <pod> --port=3000 --name=frontend`  - Creates a service

`kubectl port-forward <pod> 8080`  - Port forward the exposed pod port to your local machine

`kubectl attach <pod> -i`  - Attach to pod

`kubectl exec <pod> command`  - Execute a command on the pod


