# Kubernetes Workload and Application Management
## Pods
The smallest deployable unit in Kubernetes containing one or more containers that share network and storage. Containers in a Pod are scheduled together and share the same lifecycle. Pods are ephemeral and typically managed by higher-level controllers.

## Deployment
Manages stateless applications by creating and updating ReplicaSets to ensure desired number of Pod replicas. Provides rolling updates, rollbacks, and scaling capabilities for applications that don't require persistent storage. Most commonly used controller for web applications and APIs.

## ReplicaSet
Ensures a specified number of identical Pod replicas are running at any given time. Usually managed automatically by Deployments rather than created directly. Replaces failed Pods and maintains the desired replica count.

## StatefulSets
Manages stateful applications that require stable network identities, persistent storage, and ordered deployment/scaling. Each Pod gets a unique, persistent identifier and its own storage volume. Used for databases, distributed systems, and applications requiring stable hostnames.

## DaemonSet
Ensures that all (or selected) nodes run a copy of a specific Pod, typically for node-level services. Automatically schedules Pods on new nodes and removes them when nodes are deleted. Commonly used for monitoring agents, log collectors, and storage daemons.

## Job
Creates one or more Pods to run a task to completion, ensuring successful termination of the workload. Handles retries for failed Pods and tracks completion status. Used for batch processing, data migrations, and one-time tasks.

## CronJob
Schedules Jobs to run at specific times using cron syntax, similar to Unix cron jobs. Creates Jobs automatically based on the defined schedule and manages job history. Used for periodic tasks like backups, cleanup operations, and scheduled reports.


# Network and Service Discovery

## Service
Provides a stable network endpoint and load balancing for a set of Pods using label selectors. Acts as an abstraction layer that maintains a consistent IP address and DNS name even when underlying Pods are replaced. Supports different types like ClusterIP (internal), NodePort (external access via node), and LoadBalancer (cloud provider integration). Essential for enabling communication between microservices and external access to applications.

## Ingress
Manages external HTTP/HTTPS access to services within a cluster, acting as a reverse proxy and load balancer. Provides features like SSL termination, path-based routing, host-based routing, and centralized access control. Requires an Ingress Controller (like NGINX, Traefik, or cloud-specific controllers) to implement the actual routing rules. More cost-effective than using multiple LoadBalancer services for external access.

## NetworkPolicy
Defines rules for controlling network traffic flow between Pods, namespaces, and external endpoints at the IP and port level. Acts as a firewall for Kubernetes clusters, allowing you to implement micro-segmentation and zero-trust networking. Requires a CNI (Container Network Interface) plugin that supports NetworkPolicies like Calico, Cilium, or Weave. By default, all traffic is allowed until NetworkPolicies are applied to restrict communication.

## Endpoints
Automatically created objects that contain the actual IP addresses and ports of Pods that match a Service's selector. Kubernetes continuously updates Endpoints as Pods are created, deleted, or become ready/unready based on health checks. Can be manually created for services that point to external resources outside the cluster. Services use Endpoints to determine where to route traffic, making them a crucial component in service discovery.


# Kubernetes Volume concepts

## Volume
A directory accessible to containers in a Pod that can persist data beyond container restarts and be shared between containers. Volumes are tied to the Pod's lifecycle and are destroyed when the Pod is deleted. Supports various types like emptyDir (temporary), hostPath (node storage), configMap/secret (configuration data), and cloud storage (AWS EBS, GCP PD).

## PersistentVolume (PV)
A cluster-wide storage resource provisioned by administrators or dynamically created by storage classes, independent of any Pod lifecycle. Represents actual storage (like AWS EBS, NFS, local disk) with specific capacity, access modes, and retention policies. PVs exist independently and can be reused by different PVCs even after the original Pod is deleted.

## PersistentVolumeClaim (PVC)
A request for storage by a user/Pod that binds to an available PersistentVolume matching the specified requirements (size, access mode, storage class). Acts as an abstraction layer allowing Pods to request storage without knowing the underlying storage details. Once bound to a PV, the PVC can be mounted into Pods and provides persistent storage that survives Pod restarts and rescheduling.

## StorageClass
Defines different "classes" or tiers of storage with specific provisioners, parameters, and policies for dynamic volume provisioning. Allows automatic creation of PersistentVolumes when PVCs are created, eliminating the need for manual PV provisioning. Examples include different performance tiers (SSD vs HDD), replication policies, or cloud provider-specific storage types (gp2, gp3 for AWS).
