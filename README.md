# KomposeELK

Starting up ELK stack using K8s (minikube). Below instructions are specifically for mac.

## Pre-requisites
  - Download minikube
    `brew install minikube`
  - Download kompose - utility to convert docker-compose to K8s yamls
    `brew install kompose`

## How to Kompose
Kompose is a utility to convert docker-compose to k8s yamls. It is suggested by kubernetes.io and further information can be found [here]( https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes/).

### Key command for kompose
  - **Convert:** `kompose convert` | `kompose convert -f [fileName]` 
    This command is used to convert docker-compose to k8s yamls. `kompose convert` converts the file with name docker-compose.yaml and to convert a specific file, we can use kompose convert -f [fileName]
  - Issues Encountered: 
    - *It does not identify the environment variables and ignored all the environment variables. We need to create configMaps for these env variables manually*
    - *Since environment variables are ignored, they don't end up in the converted yamls. Example: the image name with env variables - only the text would be converted and env variables would be ignored*
    
## Starting ELK with Minikube
  - Start minikube
  ```minikube start --vm=true```
  <br/>By default, minikube would start using the docker driver. Exposing the service with docker driver is a bit tricky as it requires to create a tunnel and then expose the same. For simiplicity sake, we would use VM driver. The default vm driver for MAC is hyperkit.
  - Run the following commands <br/>
  ```
     kubectl apply -f elasticsearch-persistentvolumesclient.yaml
     kubectl apply -f elasticsearch-deployment.yaml
     kubectl apply -f kibana-deployment.yaml
  ```
