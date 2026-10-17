# K8s — Local Kubernetes with Kind (Kubernetes-in-Docker)

Hands-on notes for spinning up **local Kubernetes clusters** with **Kind** (Kubernetes-in-Docker),
installing **kubectl**, defining a **multi-node cluster**, and enabling the **Kubernetes Dashboard**.

> This is a personal learning-notes repository — a concise, copy-paste reference for getting a
> local Kubernetes environment running quickly. It is not a framework or a tool; it is a set of
> tested commands and example manifests collected while learning and testing Kubernetes.

## What is this?

A short, practical cheat sheet that covers the fastest path to a local Kubernetes cluster:

- **Kind** — run Kubernetes clusters inside Docker containers (nodes are containers, not VMs).
- **kubectl** — install and use the Kubernetes command-line client.
- **Multi-node cluster** — an example Kind config with one control-plane and two workers.
- **Kubernetes Dashboard** — enable it and expose it as a service (see
  [Kubernetes-Dashboard.md](Kubernetes-Dashboard.md)).

## Who is this for?

Developers and students who want a **fast, disposable local Kubernetes cluster** for testing
applications, controllers, and Kubernetes itself — without the overhead of VM-based tools like
minikube or microk8s.

## Why Kind?

- Kind is **K**ubernetes-**in**-**D**ocker.
- It uses Docker containers to simulate nodes.
- Boots a cluster in ~30 seconds.
- Ideal for testing Kubernetes, applications, controllers, and for training.

## Prerequisites

- **Docker** installed and running.
- A Linux/macOS shell (commands below target Linux x86_64).

## Quickstart

### 1. Install Kind

```bash
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.19.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

> `v0.19.0` is the version used in these notes. Check the
> [Kind releases page](https://github.com/kubernetes-sigs/kind/releases) for the latest version.

### 2. Create a cluster

List existing clusters:

```bash
kind get clusters
```

Create a cluster from a config file:

```bash
kind create cluster --config=test_config.yaml --name my_cluster
```

Example `test_config.yaml` — a three-node cluster (one control-plane, two workers):

```yaml
# three node (two workers) cluster config
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

Delete the cluster when done:

```bash
kind delete cluster --name my_cluster
```

### 3. Install and use kubectl

`kubectl` is the official Kubernetes command-line tool for managing and controlling
Kubernetes resources.

```bash
sudo snap install kubectl --classic
kubectl version --client
kubectl config view
```

## Kubernetes Dashboard

Steps to enable the Kubernetes Dashboard and expose it (via `NodePort` or `LoadBalancer`)
are in [Kubernetes-Dashboard.md](Kubernetes-Dashboard.md).

## FAQ

**How is Kind different from minikube or microk8s?**
Kind runs each Kubernetes node as a Docker container instead of a virtual machine, so clusters
boot faster (~30s) and are easy to create and throw away.

**Can I run a multi-node cluster locally with Kind?**
Yes. Use a Kind config file that lists multiple `nodes` (see the example above) to get a
control-plane plus worker nodes.

**Is this a production tool?**
No. These are learning notes and Kind itself is intended for local development, testing, and CI —
not production workloads.

## References

- Kind quick start: https://kind.sigs.k8s.io/docs/user/quick-start/
- Kubernetes: https://kubernetes.io/
- kubectl: https://kubernetes.io/docs/reference/kubectl/

## Companion video

Walkthrough on YouTube: [watch here](https://youtu.be/srXZX7paFoc)

## License

Licensed under the [Apache License 2.0](LICENSE).

<!-- legal-notice: start -->
### Legal notice and responsible use

The materials in this repository are made available without warranties to the extent permitted by applicable law. **Please read the [Disclaimer and Responsible-Use Notice](DISCLAIMER.md)** before relying on or deploying them. This notice does not change any existing software license or limit rights that cannot legally be waived.
<!-- legal-notice: end -->
