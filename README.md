# Jenkins/Kubernetes/Node-Red - CI/CD Pipeline Demo Using Jenkins Kubernetes Plugin

Why Jenkins On Kubernetes:
1. Containerized component
2. High Availability
3. Dynamic scaling
4. Enforce memory and cpu

## Pre-reqs

Standard Kubernetes Cluster or Minikube with Kubectl & Helm Installed
```bash
minikube addons enable ingress
minikube addons enable registry
brew install kubectl
brew install kubernetes-helm
helm init --wait
```

## Deploy and Configure Jenkins

Get existing helm chart values using helm inspect.

```bash
helm inspect values stable/jenkins > jenkins.values
```

Override values as mentioned in overrides.yaml file & install helm with the overridden values

```bash
helm install stable/jenkins --values overrides.yaml --name jenkins --namespace jenkins
```

Jenkins UI can be accessed using the url 'http://localhost:NODEPORT'. Password will be password mentioned in overrides.yaml file.

## Configure Jenkins

1. Jenkins >> Credentials create a credentials with Kind "Kubernetes Service Account"
2. Manage Jenkins >> Configure Systems , test Kubernetes connection with the above credential.
3. Now Jenkins Kubernetes Plugin is ready to USE

## Deploy app

1. Create a pipline job with a fork of this repository as the Git source for the pipeline. Refer Jenkinsfile for the pipeline job.
2. Create credentials in Jenkins for Dockerhub connectivity (id: dockerhub)
3. Clicking *Build now* will run the pipeline.
4. Run "kubectl get svc" to get the NodePort of Node-Red UI.

# nr-kube-pipeline
