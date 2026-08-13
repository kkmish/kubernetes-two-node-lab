# Two-Node Kubernetes Lab

A basic hands-on Kubernetes lab built using two Ubuntu virtual machines in VMware Workstation.

## Architecture

- **Control Plane:** Ubuntu — 192.168.1.150
- **Worker Node:** Ubuntu — 192.168.1.151
- **Kubernetes:** v1.33
- **Container Runtime:** CRI-O
- **Container Network:** Calico CNI
- **Test Application:** Nginx

## What I Implemented

- Configured static IP networking for the Kubernetes nodes
- Disabled swap and enabled IPv4 forwarding
- Installed kubeadm, kubelet and kubectl
- Installed and configured CRI-O as the container runtime
- Initialized the Kubernetes control plane using kubeadm
- Installed Calico CNI for pod networking
- Joined a worker node to the cluster
- Verified both nodes reached Ready state
- Created an Nginx Deployment
- Verified that the Nginx Pod was scheduled on the worker node
- Tested the Nginx application using the Pod IP

## Cluster Verification

```bash
kubectl get nodes
kubectl get pods -o wide
```

The completed cluster consisted of one control-plane node and one worker node, with both nodes in the `Ready` state.

## Nginx Deployment

```bash
kubectl create deployment nginx-app --image=nginx
kubectl get deployments
kubectl get pods -o wide
```

Kubernetes scheduled the Nginx Pod on the worker node. The application was verified using:

```bash
curl <pod-ip>
```

which returned the Nginx welcome page.

## Troubleshooting

During the worker-node join process, the original kubeadm bootstrap token was no longer valid. A new join command was generated from the control plane:

```bash
kubeadm token create --print-join-command
```

The worker then successfully joined the cluster using the new token.

## Skills Practiced

Kubernetes fundamentals, Linux administration, kubeadm, kubelet, kubectl, CRI-O, Calico CNI, container networking, deployments, pods, and basic Kubernetes troubleshooting.

> This is a learning/lab project intended to demonstrate basic hands-on familiarity with Kubernetes rather than production Kubernetes administration.
