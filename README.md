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
### Kubeadm
```
sudo apt-get update
# apt-transport-https may be a dummy package; if so, you can skip that package
sudo apt-get install -y apt-transport-https ca-certificates curl gpg

# If the directory `/etc/apt/keyrings` does not exist, it should be created before the curl command, read the note below.
# sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.34/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

# This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.34/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

sudo systemctl enable --now kubelet

# Run this after install docker
wget https://raw.githubusercontent.com/Mirantis/cri-dockerd/master/packaging/systemd/cri-docker.service
wget https://raw.githubusercontent.com/Mirantis/cri-dockerd/master/packaging/systemd/cri-docker.socket
sudo mv cri-docker.socket cri-docker.service /etc/systemd/system/
sudo sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service
```
### Setup Kubernetes
For First time running in the ***`Master node***
```
sudo kubeadm init --apiserver-advertise-address=10.38.240.95 --pod-network-cidr=10.244.0.0/16
```
Then to start using your cluster, you need to run the following as a regular user:
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Then you can join any number of worker nodes by running the following on each as root:
```
sudo kubeadm token create --print-join-command
```

Init for KUBECONFIG:
```
export KUBECONFIG=/path/to/config.yaml
```
kubeadm join 10.38.240.95:6443 --token mlpjxc.4mi9tn8slbp6nc5a --discovery-token-ca-cert-hash sha256:2c229808dd16f17d7920724f8604b2df29ce3450eaeb91d68c32aae05e19df0f