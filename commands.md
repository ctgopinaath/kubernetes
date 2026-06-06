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

# ConfigMaps

```bash
kubectl get cm
kubectl get cm -A

kubectl describe cm <configmap>

kubectl edit cm <configmap>

kubectl create configmap app-config \
--from-file=config.properties

kubectl create configmap app-config \
--from-literal=env=dev

kubectl create configmap app-config \
--from-env-file=.env

kubectl delete cm <configmap>

kubectl patch cm <configmap>

kubectl get cm -o yaml
kubectl get cm -o json
```

---

# Secrets

```bash
kubectl get secrets
kubectl get secrets -A

kubectl describe secret <secret>

kubectl edit secret <secret>

kubectl create secret generic my-secret \
--from-literal=username=admin \
--from-literal=password=password

kubectl create secret generic my-secret \
--from-file=secret.txt

kubectl create secret tls tls-secret \
--cert=tls.crt \
--key=tls.key

kubectl create secret docker-registry regcred \
--docker-server=<server> \
--docker-username=<user> \
--docker-password=<password>

kubectl get secret my-secret -o yaml
kubectl get secret my-secret -o json

kubectl get secret my-secret \
-o jsonpath='{.data.password}' | base64 -d

kubectl delete secret my-secret
```

---

# Service Accounts

```bash
kubectl get sa
kubectl get sa -A

kubectl describe sa default

kubectl create sa app-sa

kubectl create token app-sa

kubectl delete sa app-sa

kubectl get sa app-sa -o yaml
```

---

# Resource Quotas

```bash
kubectl get quota
kubectl get quota -A

kubectl describe quota

kubectl create quota compute-quota \
--hard=cpu=4,memory=8Gi

kubectl delete quota compute-quota
```

---

# Limit Ranges

```bash
kubectl get limitrange
kubectl get limitrange -A

kubectl describe limitrange

kubectl delete limitrange <name>
```

---

# Endpoints

```bash
kubectl get endpoints
kubectl get ep

kubectl get endpoints -A

kubectl describe endpoints <name>
```

---

# EndpointSlices

```bash
kubectl get endpointslices
kubectl get endpointslices -A

kubectl describe endpointslice <name>

kubectl get endpointslices -o yaml
```

---

# Ingress

```bash
kubectl get ingress
kubectl get ingress -A

kubectl describe ingress <ingress>

kubectl delete ingress <ingress>

kubectl get ingressclass
kubectl describe ingressclass <class>
```

---

# Pod Disruption Budgets (PDB)

```bash
kubectl get pdb
kubectl get pdb -A

kubectl describe pdb <name>

kubectl delete pdb <name>
```

---

# Priority Classes

```bash
kubectl get priorityclass

kubectl describe priorityclass <name>

kubectl delete priorityclass <name>
```

---

# Runtime Classes

```bash
kubectl get runtimeclass

kubectl describe runtimeclass <name>

kubectl delete runtimeclass <name>
```

---

# Horizontal Pod Autoscaler (HPA)

```bash
kubectl get hpa
kubectl get hpa -A

kubectl describe hpa <name>

kubectl autoscale deployment nginx \
--cpu-percent=70 \
--min=2 \
--max=10

kubectl delete hpa nginx
```

---

# Vertical Pod Autoscaler (VPA)

```bash
kubectl get vpa
kubectl get vpa -A

kubectl describe vpa <name>
```

---

# Network Policies

```bash
kubectl get networkpolicy
kubectl get networkpolicy -A

kubectl describe networkpolicy <policy>

kubectl delete networkpolicy <policy>
```

---

# CSI Drivers

```bash
kubectl get csidriver
kubectl get csinode

kubectl describe csidriver <name>

kubectl get csistoragecapacity -A
```

---

# Volume Snapshots

```bash
kubectl get volumesnapshot
kubectl get volumesnapshotclass
kubectl get volumesnapshotcontent

kubectl describe volumesnapshot <name>

kubectl describe volumesnapshotclass <name>

kubectl describe volumesnapshotcontent <name>
```

---

# API Services

```bash
kubectl get apiservice
kubectl get apiservice -A

kubectl describe apiservice <name>
```

---

# Validating Webhooks

```bash
kubectl get validatingwebhookconfigurations

kubectl describe validatingwebhookconfiguration <name>
```

---

# Mutating Webhooks

```bash
kubectl get mutatingwebhookconfigurations

kubectl describe mutatingwebhookconfiguration <name>
```

---

# Leases

```bash
kubectl get leases
kubectl get leases -A

kubectl describe lease <name>
```

---

# Events

```bash
kubectl get events
kubectl get events -A

kubectl get events \
--sort-by=.metadata.creationTimestamp

kubectl get events \
--field-selector type=Warning
```

---

# Labels

```bash
kubectl label pod <pod> env=prod

kubectl label node <node> env=prod

kubectl label deployment <deployment> env=prod

kubectl get pods -l env=prod

kubectl get all -l env=prod
```

---

# Annotations

```bash
kubectl annotate pod <pod> owner=devops

kubectl annotate deployment nginx \
description="production"

kubectl get pod <pod> \
--show-managed-fields
```

---

# Selectors

```bash
kubectl get pods -l app=nginx

kubectl get pods -l app!=nginx

kubectl get pods -l 'env in (prod,dev)'

kubectl get pods -l 'env notin (prod)'
```

---

# Output Formats

```bash
kubectl get pods -o yaml

kubectl get pods -o json

kubectl get pods -o wide

kubectl get pods -o name

kubectl get pods \
-o custom-columns=NAME:.metadata.name

kubectl get pods \
-o jsonpath='{.items[*].metadata.name}'
```

---

# CRDs

```bash
kubectl get crd

kubectl describe crd <crd>

kubectl api-resources

kubectl explain <crd>
```

---

# Ephemeral Containers

```bash
kubectl debug pod/<pod>

kubectl debug pod/<pod> \
-it \
--image=busybox

kubectl debug node/<node>
```

---

# API Discovery

```bash
kubectl api-resources

kubectl api-versions

kubectl explain pod

kubectl explain pod.spec

kubectl explain deployment.spec.template.spec
```

---

# Complete Cluster Inventory

```bash
kubectl api-resources --verbs=list --namespaced -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found -A

kubectl api-resources --verbs=list --namespaced=false -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found
```
