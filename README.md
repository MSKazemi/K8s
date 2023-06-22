# K8s on Kind
Kind is a Kubernetes SIGs project that allows you to run local Kubernetes clusters using Docker containers. As its name suggests, kind spins up k8s clusters in Docker containers called nodes. This results in faster Kubernetes set up compared to VM-based Kubernetes like minikube and microk8s.

- Kind is **K**ubernetes-**in**-**D**ocker
- It uses Docker containers to simulate nodes
- Boots a cluster in ~ 30s
- Testing Kubernetes/applications/controllers/training




## Kind Installation

`[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.19.0/kind-linux-amd64`

`chmod +x ./kind`

`sudo mv ./kind /usr/local/bin/kind`


`kind get clusters`

`kind create cluster --config=test_config.yaml --name my_cluster`



```yaml
# three node (two workers) cluster config
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

`kind delete cluster --name my_cluster`

## Kubectl
kubectl is a command-line tool used for interacting with Kubernetes clusters. It is part of the official Kubernetes project and is used to manage and control Kubernetes resources.

`sudo snap install kubectl --classic`

`kubectl version --client`

`kubectl config view`


https://kind.sigs.k8s.io/docs/user/quick-start/

## YouTube Video
Check it out [here](https://youtu.be/srXZX7paFoc)!

