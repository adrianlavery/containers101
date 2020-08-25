# Kubernetes demo script

## Create an AKS cluster
```
# Create a resource group if required
az group create --location westeurope --name containers101

# Create an AKS cluster. Note this can take around ten minutes
az aks create --resource-group containers101 --name myAKSCluster --node-count 1 --generate-ssh-keys
```
Have a look in the Azure portal and notice that there are two new resource groups. One named 'containers101' which contains your AKS cluster and one named 'MC_containers101_myAKSCluster_westeurope' which contains the cluster nodes in a virtual machine scaleset.

## Connect to your AKS cluster
```
az aks get-credentials --resource-group containers101 --name myAKSCluster
```

## Look at the existing pods on AKS
```
kubectl get pods
```

## Deploy a pod on AKS
```
kubectl apply -f pod.yaml

# List the pods
kubectl get pods
```
## Deploy multiple pods on AKS
```
kubectl apply -f multiplePods.yaml

# List the pods
kubectl get pods

# List the deployments
kubectl get deployment
```

## Container self healing

### Delete original azure-vote pod
```
# List the pods
kubectl get pods

# Delete the original pod
kubectl delete pod azure-vote
```
Now list the pods again using `kubectl get pods` and notice that the azure-vote pod doesn't get recreated.

### Delete one of the pods deployed via the deployment
```
kubectl delete pod azure-vote-back-6b4c4f4774-47nz2
```

Now list the pods again using `kubectl get pods` and notice you still have four pods. Notice the age of one will only be a few seconds. This is the pod that has self-healed.


## Deploy service on AKS
```
kubectl apply -f service.yaml

# List the services
kubectl get service
```

# Deploy the full application

First off, let's clean up everything we've added.
```
# Delete the service
kubectl delete service azure-vote-back
# There should only be a kubernetes service
kubectl get service

# Delete the deployment
kubectl delete deployment azure-vote-back
# There should be no pods in the default namespace
kubectl get pods
```
Now deploy the app in it's own namespace
``` 
# Create namespace
kubectl create namespace voting-app
# deploy app
kubectl apply -f votingApp.yaml
```
Have a look at the resources we have created
```
kubectl get all --namespace voting-app
```
Note you should have four pods, two services,two deployments and two replicasets.

## See the application running

Find the public IP address of the front end
```
kubectl get service azure-vote-front --namespace voting-app
```
Find the external IP address browse to it in your web browser http://[EXTERNAL-IP] e.g. http://51.124.72.161