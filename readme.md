# Kubernetes Pods

## Overview
A Pod is the smallest deployable unit in Kubernetes. It represents a single instance of a running process in your cluster and serves as the basic execution unit for applications.

## Key Characteristics

### Single or Multiple Containers
- A Pod can contain one or more containers
- Containers within a Pod are tightly coupled and share resources
- Most commonly, a Pod contains just one container

### Shared Resources
- **Network**: All containers in a Pod share the same IP address and port space
- **Storage**: Containers can share volumes mounted to the Pod
- **Lifecycle**: All containers in a Pod are scheduled together and live/die together

### Ephemeral Nature
- Pods are ephemeral and disposable
- Each Pod gets a unique IP address (within the cluster)
- When a Pod dies, it's replaced with a new Pod (with a new IP)

## Pod Lifecycle

### Pod Phases
- **Pending**: Pod has been accepted but containers aren't running yet
- **Running**: Pod is bound to a node and at least one container is running
- **Succeeded**: All containers have terminated successfully
- **Failed**: All containers have terminated, at least one failed
- **Unknown**: Pod state cannot be determined

### Container States
- **Waiting**: Container is waiting to start
- **Running**: Container is executing normally
- **Terminated**: Container has finished execution

## Basic Pod Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
    environment: production
spec:
  containers:
  - name: nginx
    image: nginx:1.21
    ports:
    - containerPort: 80
      name: http
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
