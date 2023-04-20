# Blog-Application


**In this project, we worked  with Docker and Kubernetes to make an easily deployable and portable blogging web-app using Flask and MongoDB.**  

The microservices architecture will deploy a Kubernetes cluster with a mongodb server pod fronted with a web admin interface and a pod to run the flask app.

## Pre-Requisites/ Pre-Installation:
1. Docker ([Windows](https://docs.docker.com/desktop/windows/install/) | [Ubuntu](https://docs.docker.com/engine/install/ubuntu/#:~:text=Install%20from%20a%20package&text=Go%20to%20https%3A%2F%2Fdownload,version%20you%20want%20to%20install) | [MacOS](https://docs.docker.com/desktop/mac/install/))
2. Kubernetes ([Windows](https://birthday.play-with-docker.com/kubernetes-docker-desktop/) | [Ubuntu](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) | [MacOS](https://birthday.play-with-docker.com/kubernetes-docker-desktop/))

## File Structure
```
.
|-- README.md
|-- app
|   |-- app.py
|   |-- requirements.txt
|   `-- templates
|       |-- base.html
|       |-- create-post.html
|       |-- edit-post.html
|       `-- home.html
|-- configmap.yaml
|-- deployments.yaml
|-- execute.bat
|-- cleanup.bat
|-- flask-app-image.dockerfile
|-- secret.yaml
`-- services.yaml
```
The `app` directory contains all the code pertaining to the flask app. You are only required to configure the mongo connection string variables as specified in `app.py`.  
The `flask-app-image.dockerfile` should specify the insructions to assemble the docker image for the flask app.  
The `.yaml` files in the root directory are to specify the kubernetes manifests that will bring up your microservices deployment of the problem statement.



## How to run 
 1. Make sure that kubernets is up and running (Open docker desktop > settings > kubernets)
 

 2. Pulling Resources for that you need to Execute below  Commands 
          "docker pull python"
          "docker pull mongo-express"
          "docker pull mongo"
          "pause"
          

 3. After executing  above commands now we will build the docker image and create kubernet cluster
 

 4. Command to build a docker image 
          "docker build . -f flask-app-image.dockerfile -t blogapp:1.0" 
 

 5. Commands to create kubernet cluster  (all the below files are present in above repository)
 
         " kubectl apply -f secret.yaml "
         " kubectl apply -f configmap.yaml "
         " kubectl apply -f services.yaml "
         " kubectl apply -f deployments.yaml "
    
    
    Wait for 10Sec for cluster to be up and running after that execute below commands 
    
          " kubectl get pod " 

 6. After succesfull creation of kubernet cluster Execute the below commands 
 
    
          " start  "http://localhost:5001"  "
          " pause "
     
     
     Wait till the web page opens otherwise Click on the link you will be directed to web-application which is running on localhost on port number of 5001


 7. In Web page you can edit delete and update the blogs. 


 8. After all the operations make sure that you remove all the images pods and deployments
 
    Command to remove the pods images and deployments 
    
          " kubectl delete pod --all "
          " kubectl delete deploy --all "
          " docker rmi -f blogapp:1.0 "
