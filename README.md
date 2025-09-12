# My Final Project

### Depedency
```
Docker
Docker-Compose
git
curl
k3s
Hyprledger Bevel
Hyprledger Fabric
```

###  Installation Guide
```
git clone https://github.com/hyperledger-bevel/bevel.git
cd bevel
git clone git clone git@github.com:NopNopBeta/build.git
```

### Build the provisioning image
```
docker run -it -v $(pwd):/home/bevel/ --network="host" ghcr.io/hyperledger/bevel-build:latest
```

---
### Kubernetes Cluster

k3s master
```
# Instalation 
curl -sfL https://get.k3s.io | sh -

# check Token
sudo cat /var/lib/rancher/k3s/server/node-token
```
k3s Worker
```
# Instalation
curl -sfL https://get.k3s.io | K3S_URL=https:<IP Address>:6443 K3S_TOKEN=<TOKEN> sh 
