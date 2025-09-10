# MasterLedger

Depedency
```
Docker
Docker-Compose
git
curl
k3s
Hyprledger Bevel
Hyprledger Fabric
```

Installation for Hyprledger Bevel in the Master node

```
git clone https://github.com/hyperledger-bevel/bevel.git

cd bevel

# Build the provisioning image
docker build . -t ghcr.io/hyperledger/bevel-build
```

Running Network.yaml
```
# Run the provisioning scripts
docker run -it -v $(pwd):/home/bevel/ ghcr.io/hyperledger/bevel-build
```

**Kubernetes Cluster**

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
curl -sfL https://get.k3s.io | K3S_URL=https:<IP Addres>:6443 K3S_TOKEN=
