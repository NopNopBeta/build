# My Final Project

## Depedency
```
Docker
Docker-Compose
cri-dockerd
git
curl
wget
k8s
Hyprledger Bevel
Hyprledger Fabric
```

##  Installation Guide
```
git clone https://github.com/hyperledger-bevel/bevel.git
cd bevel
git clone git clone git@github.com:NopNopBeta/build.git
```

## Build the provisioning image
```
docker run -it -v $(pwd):/home/bevel/ --network="host" ghcr.io/hyperledger/bevel-build:latest
```

---
## Kubernetes Cluster
### K8S 
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

### Minikube
```
# Create the multi-node cluster directly (all nodes will have same resources)
minikube start --profile=kubernetes --nodes=3 --cpus=2 --memory=2048 --driver=docker

# Verify the cluster
kubectl get nodes

# Optional: Label the nodes with custom names (for identification)
kubectl label node kubernetes node-role.kubernetes.io/master-node=masternode
kubectl label node kubernetes-m02 node-role.kubernetes.io/worker-node=workernode1  
kubectl label node kubernetes-m03 node-role.kubernetes.io/worker-node=workernode2
```