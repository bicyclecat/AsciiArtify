# **Kubernetes local-development tools comparative analysis**
## Considered tools:

__Minikube.__ A popular open-source tool designed for local Kubernetes cluster development. Its main purpose is to enable developers to set up a single-node Kubernetes cluster on their local machines. Minikube automates the process of provisioning and managing the Kubernetes cluster, making it easy for developers to test applications in a Kubernetes environment locally. Unlike KIND and k3d, it comes with integrated support of Kubernetes UI dashboard.

__KIND (Kubernetes IN Docker).__ Another tool tailored for local Kubernetes development but takes a different approach by creating clusters using Docker containers as nodes. The main purpose of KIND is to provide a fast and consistent way to spin up Kubernetes clusters for testing and development. KIND stands out for its automation capabilities, allowing users to define cluster configurations using simple YAML files. Although KIND primarily focuses on cluster provisioning, it integrates well with external tools for monitoring and logging, making it a flexible choice for developers who require more extensive cluster management capabilities.

__k3d.__ A tool that simplifies the deployment of Kubernetes clusters using Docker. Its main purpose is to offer a fast and lightweight alternative for local Kubernetes development. K3d stands out for its automation capabilities, allowing users to create single or multi-node Kubernetes clusters with ease. Additionally, k3d includes features for cluster management, such as scaling nodes up or down. While it doesn't provide built-in monitoring features, it seamlessly integrates with monitoring tools, giving developers the flexibility to choose their preferred monitoring solution for the Kubernetes clusters created with k3d.

## Characteristics

| Characteristic           | Minikube                              | KIND                                  | k3d                                   |
| ------------------------ | ------------------------------------- | ------------------------------------- | ------------------------------------- |
| **OS support**           | Linux, macOS, Windows                 | Linux, macOS, Windows                 | Linux, macOS, Windows                 |
| **Architecture support** | x86, amd64                            | amd64                                 | amd64, ARM                            |
| **Monitoring**           | Integrated dashboard support          | Needs external monitoring tools       | Needs external monitoring tools       |
| **Podman support**       | Experimental, realtively simple       | Relatively complicated                | Experimental, realtively complicated  |

## Advantages and disadvantages

| Tool                     | Advantages                                                                                                                                                                     | Disadvantages                                                                                                             |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| **Minikube**             | <ul><li>Has integrated support for the Kubernetes Dashboard UI</li><li>VM provider agnostic</li></ul>                                                                          | <ul><li>Limited cluster scalability</li><li>Not recommended for production environments</li></ul>                         |
| **KIND**                 | <ul><li>Fast cluster creation</li><li>Convenient cluster configuration</li></ul>                                                                                               | <ul><li>Strictly dependent on Docker</li><li>High memory requirements (8GB recommended)</li></ul>                         |
| **k3d**                  | <ul><li>Very low system resource requirements</li><li>Fast iteration (good for development)</li><li>Convenient cluster configuration and replication (config file)</li></ul>   | <ul><li>Relatively low feature set</li><li>May not be recommended for production environments</li></ul>                   |

## Minikube usage example

### Installation
To get started, please follow the [Minikube installation guide](https://minikube.sigs.k8s.io/docs/start/).
### Starting Minikube
To create a Minikube cluster or start an existing one, run:
```bash
minikube start
```
### Get Cluster Status
To get information about your cluster, run:
```bash
minikube status
```
### Get configuration
To get Kubernetes information about your cluster, run:
```bash
minikube kubectl -- get config
```
### Minikube Dashboard
Minikube has integrated support for the Kubernetes Dashboard UI. You can access it like this:
```bash
minikube dashboard
```
Or you can make Minikube to generate a dashboard URL without opening the web browser:
```bash
minikube dashboard --url
```
### Stopping Minikube cluster
```bash
minikube stop
```
### Removing a cluster
Optionally, you can also remove your Minikube cluster by running:
```bash
minikube delete
```
![Minikube usage demo](../media/minikube-usage-demo.gif)

## KIND usage example

### Installation
To get started, please follow the [KIND installation guide](https://kind.sigs.k8s.io/docs/user/quick-start/#installation).
### Creating a cluster
To create a cluster with a default name "kind" and a prebuilt image, run:
```bash
kind create cluster
```
Or you may create a cluster with your custom name and image:
```bash
kind create cluster --name my-cluster --image=...
```
### Get clusters list
You can get the list of your clusters:
```bash
kind get clusters
```
### Interacting with clusters
To interact with a specific cluster, you only need to specify its name as a context in kubectl, e.g. "my-cluster":
```bash
kubectl cluster-info --context kind-my-cluster
```
### Deleting a cluster
To delete your cluster, run:
```bash
kind delete cluster
```
or, if you gave it a name, then you can delete it like this:
```bash
kind delete cluster --name my-cluster
```
![KIND usage demo](../media/kind-usage-demo.gif)

## k3d usage example
### Installation
To get started, please follow the [k3d installation guide](https://github.com/k3d-io/k3d)
### Creating a cluster
To create a k3d cluster with a name, e.g. "my-cluster", run:
```bash
k3d cluster create my-cluster
```
### Check k3d version
To check installed k3d version, run:
```bash
k3d --version
```
### Get cluster info
To get information about your cluster, e.g. "my-cluster", run:
```bash
kubectl cluster-info --context k3d-my-cluster
```
### Deleting a cluster
To delete your cluster, run:
```bash
k3d cluster delete my-cluster
```
![k3d usage demo](../media/k3d-usage-demo.gif)
## Conclusion
Considering the needs of developers, the recommended tool is k3d, due to its lightweight, ease of learning and high iterativity, which helps speed up the development process.
