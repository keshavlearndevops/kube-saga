# Kubernetes Architecture 

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/604c0da9-3f6b-40b9-8d12-a2b5eb515270)

- A ***Kubernetes cluster*** is composed of worker machines, referred to as nodes, which are responsible for running containerized applications. Each cluster is equipped with at least one worker node.
- These ***worker*** nodes play host to Pods, which are the fundamental components of an application's workload. The control plane takes charge of overseeing both the worker nodes and the Pods within the cluster. 
- In more advanced setups, the control plane is typically spread across multiple computers, while a cluster typically includes several nodes. This design ensures fault-tolerance and the ability to maintain high availability, making it well-suited for production environments.

## Understanding K8s Components

### Control Plane Components

The control plane components in Kubernetes are responsible for making high-level decisions about the cluster's behavior and handling various events that occur within the cluster.

- **kube-apiserver**: This is the entry point for interacting with the Kubernetes API. It exposes the Kubernetes API to users and external services. The kube-apiserver is scalable and can have multiple instances to handle incoming requests, making the system more robust and capable of handling high loads.

- **etcd**: Etcd is a distributed key-value store that acts as Kubernetes' database. It stores all the configuration and state information for the cluster. This ensures that the entire cluster has access to consistent and up-to-date data. Backing up etcd is crucial for data resilience.

- **kube-scheduler**: The scheduler is responsible for assigning workloads (Pods) to available nodes. It takes into account various factors like resource requirements, constraints, and affinity rules to make optimal placement decisions.

- **kube-controller-manager**: This component manages various controllers that watch over the state of the cluster and work to ensure that the actual state matches the desired state. Examples include the Node controller, which handles node failures, and the Job controller, which ensures tasks are completed.

- **cloud-controller-manager**: If your cluster is running on a cloud provider, this component interfaces with the cloud provider's API to manage cloud-specific resources, such as load balancers and route tables. It isolates cloud-specific logic from the core Kubernetes components.

### Node Components

Node components run on every node in the cluster and are responsible for maintaining the individual nodes and the containers running on them.

- **kubelet**: The kubelet is an agent that runs on each node. It manages containers within Pods, ensuring they are running and healthy according to the specifications in the PodSpecs. It communicates with the control plane to receive instructions about desired Pod states.

- **kube-proxy**: Kube-proxy is responsible for managing network communication for Pods. It maintains network rules that allow network traffic to reach the correct Pods. It can operate using the underlying operating system's networking mechanisms or by forwarding traffic itself.

- **Container runtime**: This is the software responsible for running containers. Kubernetes is designed to work with various container runtimes, such as Docker, containerd, and CRI-O. The runtime interacts with the hardware to start, stop, and manage containers.

### Workload Resources

Kubernetes manages various resources that represent the workloads running on the cluster:

- **Pods**: Pods are the smallest deployable units in Kubernetes. They can contain one or more containers that share network and storage resources. Pods are scheduled and managed together.

- **Services**: Services provide network access to a set of Pods, enabling communication among them. They offer load balancing and service discovery, making it easier for applications to find and communicate with each other.

- **ReplicaSets**: ReplicaSets ensure a specified number of identical Pods are running at all times. They handle scaling and self-healing by creating or terminating Pods based on the desired replica count.

- **Deployments**: Deployments manage ReplicaSets, enabling controlled updates and rollbacks of application versions. They ensure that the desired number of Pods are running and manage the transition from one version to another.

### Addons

Addons are optional features that enhance the functionality of a Kubernetes cluster:

- **DNS**: Cluster DNS provides a DNS server for Kubernetes services, enabling easy communication between services using their names.

- **Dashboard**: The Dashboard is a web-based UI for managing and troubleshooting applications and the cluster itself.

- **Container Resource Monitoring**: This addon records metrics about containers, helping with resource monitoring and performance analysis.

- **Cluster-level Logging**: This mechanism saves container logs to a centralized store, making it easier to search and analyze logs.

- **Network Plugins**: Network plugins implement the container network interface (CNI) specification, managing networking between Pods and enabling communication within the cluster.

These components collectively work to manage and orchestrate containerized applications within a Kubernetes cluster, providing features like scalability, resilience, and automation.
