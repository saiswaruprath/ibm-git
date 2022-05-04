## verify environment and command line tools inside skills terminal in IBM course, coursera:

docker --version
ibmcloud version

[ ! -d 'CC201' ] && git clone https://github.com/ibm-developer-skills-network/CC201.git- clone the required repository

## pull image from docker hub and run as container

docker images -   check images
docker pull hello-world
docker run hello-world
docker ps -a - check if container got added to list
docker container rm <container_id> - remove the container

## build the image using dockerfile

docker build . -t myimage:v1 - building the image. This goes through the dockerfile and runs all the commands step by step starting from FROM till CMD.
docker images- command will now show tagged myimage. A node image also gets created apart from helloworld and myimage as "docker build" pulled node:9.4.0-alpine image
as a base

## run the image as a container

docker run -p 8080:8080 myimage:v1 -  runs the image as a container

The output should indicate that your application is listening on port 8080. This command will continue running until it exits, 
since the container runs a web app that continually listens for requests. 
To query the app, we need to open another terminal window.

open split terminal

curl localhost:8080 - use this in second terminal window- The output should indicate that 'Your app is up and running!'.

docker stop $(docker ps -q) -- stops the container 
docker ps
exit

pos this second terminal closes, and original terminal will now allow for new commands.

## Push the image to IBM Cloud Container Registry

ibmcloud target 

The environment also created an IBM Cloud Container Registry (ICR) namespace for you. 
Since Container Registry is multi-tenant, namespaces are used to divide the registry among several users. 
Use the following command to see the namespaces you have access to:

ibmcloud cr namespaces-- shows us two namespaces, one by our username sn-labs-saiswaruprat and one just sn-labsassets

ibmcloud cr region-set us-south. -- set proper region

ibmcloud cr login -- logging in to ibm cloud registry to push images
export MY_NAMESPACE=sn-labs-$USERNAME

docker tag myimage:v1 us.icr.io/$MY_NAMESPACE/hello-world:1 -- tagging image to push

docker push us.icr.io/$MY_NAMESPACE/hello-world:1 

ibmcloud cr images - verify to see image updated

ibmcloud cr images --restrict $MY_NAMESPACE

delete project for further labs.


