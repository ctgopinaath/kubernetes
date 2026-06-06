# Kubernetes Cluster Administration Command Reference

## Overview

This document provides a comprehensive collection of Kubernetes administration commands covering:

* Cluster Management
* Control Plane Administration
* Worker Node Operations
* Workload Management
* Networking
* Storage
* Security
* RBAC
* Troubleshooting
* Monitoring
* Backup & Restore
* Cluster Auditing
* Advanced Administration

---

# Cluster Information

```bash
kubectl version
kubectl version --short
kubectl cluster-info
kubectl cluster-info dump
kubectl api-resources
kubectl api-versions
kubectl config view
kubectl config current-context
kubectl config get-contexts
kubectl config use-context <context>
kubectl config set-context --current --namespace=<ns>
kubectl config view --minify
kubectl config view --raw
kubectl auth can-i '*' '*'
kubectl auth can-i create pods
kubectl auth can-i --list
```

---

# Nodes

```bash
kubectl get nodes
kubectl get nodes -o wide
kubectl get nodes -o yaml
kubectl get nodes -o json
kubectl describe node <node>
kubectl top nodes
kubectl cordon <node>
kubectl uncordon <node>
kubectl drain <node> --ignore-daemonsets
kubectl taint nodes <node> key=value:NoSchedule
kubectl taint nodes <node> key=value:NoExecute
kubectl taint nodes <node> key=value:PreferNoSchedule
kubectl taint nodes <node> key=value:NoSchedule-
kubectl label node <node> env=prod
kubectl get node --show-labels
```

---

# Namespaces

```bash
kubectl get ns
kubectl create ns dev
kubectl delete ns dev
kubectl describe ns default
```

---

# Pods

```bash
kubectl get pods
kubectl get po
kubectl get pods -A
kubectl get pods -o wide
kubectl get pods --show-labels
kubectl get pods -w
kubectl get pods -o yaml
kubectl get pods -o json
kubectl describe pod <pod>
kubectl logs <pod>
kubectl logs -f <pod>
kubectl logs --tail=100 <pod>
kubectl logs <pod> -c <container>
kubectl exec -it <pod> -- bash
kubectl exec -it <pod> -- sh
kubectl cp file.txt pod:/tmp/
kubectl delete pod <pod>
kubectl port-forward pod/<pod> 8080:80
kubectl attach <pod>
kubectl top pod
kubectl top pods -A
```

---

# Deployments

```bash
kubectl get deploy
kubectl get deploy -A
kubectl describe deploy <deploy>
kubectl create deployment nginx --image=nginx
kubectl scale deployment nginx --replicas=5
kubectl rollout status deployment/nginx
kubectl rollout history deployment/nginx
kubectl rollout undo deployment/nginx
kubectl rollout restart deployment/nginx
kubectl set image deployment/nginx nginx=nginx:latest
kubectl edit deployment nginx
kubectl delete deployment nginx
```

---

# ReplicaSets

```bash
kubectl get rs
kubectl describe rs <rs>
kubectl delete rs <rs>
```

---

# DaemonSets

```bash
kubectl get ds
kubectl get ds -A
kubectl describe ds <ds>
kubectl rollout restart ds <ds>
kubectl delete ds <ds>
```

---

# StatefulSets

```bash
kubectl get sts
kubectl describe sts <sts>
kubectl rollout restart sts <sts>
kubectl scale sts <sts> --replicas=3
kubectl delete sts <sts>
```

---

# Jobs

```bash
kubectl get jobs
kubectl describe job <job>
kubectl delete job <job>
```

---

# CronJobs

```bash
kubectl get cronjobs
kubectl describe cronjob <cronjob>
kubectl create cronjob hello --image=busybox --schedule="*/1 * * * *"
kubectl delete cronjob <cronjob>
```

---

# Services

```bash
kubectl get svc
kubectl get svc -A
kubectl describe svc <svc>
kubectl expose deployment nginx --port=80
kubectl delete svc <svc>
```

---

# Storage

```bash
kubectl get pv
kubectl get pvc
kubectl get sc
kubectl describe pv <pv>
kubectl describe pvc <pvc>
kubectl describe sc <sc>
kubectl delete pvc <pvc>
kubectl delete pv <pv>
```

---

# RBAC

```bash
kubectl get roles
kubectl get rolebindings
kubectl get clusterroles
kubectl get clusterrolebindings
kubectl describe role <role>
kubectl describe clusterrole <clusterrole>
kubectl auth can-i create pods
kubectl auth can-i --list
```

---

# Network Policies

```bash
kubectl get networkpolicy
kubectl describe networkpolicy <policy>
```

---

# Events

```bash
kubectl get events
kubectl get events -A
kubectl get events --sort-by=.metadata.creationTimestamp
```

---

# Monitoring

```bash
kubectl top nodes
kubectl top pods
kubectl top pods -A
kubectl top pod <pod>
```

---

# Debugging

```bash
kubectl describe pod <pod>
kubectl logs <pod>
kubectl logs -f <pod>
kubectl logs --previous <pod>
kubectl exec -it <pod> -- sh
kubectl debug node/<node>
kubectl debug pod/<pod>
kubectl get events
kubectl get events -A
```

---

# ETCD Administration

```bash
ETCDCTL_API=3 etcdctl endpoint health
ETCDCTL_API=3 etcdctl endpoint status
ETCDCTL_API=3 etcdctl member list
ETCDCTL_API=3 etcdctl snapshot save backup.db
ETCDCTL_API=3 etcdctl snapshot status backup.db
```

---

# Kubeadm Administration

```bash
kubeadm version
kubeadm config view
kubeadm token list
kubeadm certs check-expiration
kubeadm certs renew all
kubeadm upgrade plan
kubeadm upgrade apply v1.xx.x
kubeadm reset
```

---

# Component Versions

```bash
kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.kubeletVersion}'
kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.kubeProxyVersion}'
kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.containerRuntimeVersion}'
kubectl get pods -n kube-system -o wide
kubectl get componentstatuses
```

---

# Certificates

```bash
kubectl get csr
kubectl certificate approve <csr>
kubectl certificate deny <csr>
kubectl delete csr <csr>
```

---

# CRDs

```bash
kubectl get crd
kubectl describe crd <crd>
kubectl api-resources
```

---

# API Server Health

```bash
kubectl get --raw='/healthz'
kubectl get --raw='/livez'
kubectl get --raw='/readyz'
kubectl get --raw='/metrics'
kubectl get --raw='/version'
```

---

# Advanced Cluster Audit

```bash
kubectl get nodes -o yaml
kubectl get pods -A -o wide
kubectl get deploy -A
kubectl get ds -A
kubectl get sts -A
kubectl get svc -A
kubectl get ingress -A
kubectl get pvc -A
kubectl get pv
kubectl get sa -A
kubectl get role -A
kubectl get rolebinding -A
kubectl get clusterrole
kubectl get clusterrolebinding
kubectl get networkpolicy -A
kubectl get quota -A
kubectl get limitrange -A
kubectl get events -A
kubectl get crd
kubectl get apiservices
```

---

# Complete Cluster Inventory

```bash
kubectl api-resources --verbs=list --namespaced -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found -A

kubectl api-resources --verbs=list --namespaced=false -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found
```
