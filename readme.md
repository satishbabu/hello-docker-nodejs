#NodeJs app Docker locally on Windows 10 Home edition


##Setup:
1. Installed virutalbox
2. Downloaded minikube.exe and ran it from cmd line - `minikube start --vm-driver=virtualbox`.  It downloads and installs the required VM.
3. Download Docker desktop for Windows.  It was a zip file name docker-17.09.0-ce.zip.  I extracted only Docker.exe for my purpose.
4. Run `minikube docker-env | Invoke-Expression` to set the environment variables in powershell to connect to minikube from docker CLI

All this had to be done because the Hyper-V is not available on Windows Home edition. So, Docker on Windows can not be installed directly.

## Build container and run

1. To build the container run the following 
`docker build .`


2. Above lists the container id.  Launch the container using the id
`docker run -p 3000:3000 f5ec8a4a7ce2`


3. Visit the website using browser or run curl command.  Get the IP address of the minikube VM by running 
`minikube docker-env`
`curl xx.xx.xx.xx:3000`




