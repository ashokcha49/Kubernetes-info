# Kubernetes Workload Resources - Quick Reference

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
