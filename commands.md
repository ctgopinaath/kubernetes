################################################################################
# KUBERNETES CLUSTER ADMINISTRATION - COMMAND CHEAT SHEET
# BEGINNER TO ADVANCED
# ONLY COMMANDS
################################################################################

############################
# CLUSTER INFORMATION
############################

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

############################
# NODES
############################

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

############################
# NAMESPACES
############################

kubectl get ns
kubectl create ns dev
kubectl delete ns dev
kubectl describe ns default

############################
# PODS
############################

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

############################
# DEPLOYMENTS
############################

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

############################
# REPLICASETS
############################

kubectl get rs
kubectl describe rs <rs>
kubectl delete rs <rs>

############################
# DAEMONSETS
############################

kubectl get ds
kubectl get ds -A
kubectl describe ds <ds>
kubectl rollout restart ds <ds>
kubectl delete ds <ds>

############################
# STATEFULSETS
############################

kubectl get sts
kubectl describe sts <sts>
kubectl rollout restart sts <sts>
kubectl scale sts <sts> --replicas=3
kubectl delete sts <sts>

############################
# JOBS
############################

kubectl get jobs
kubectl describe job <job>
kubectl delete job <job>

############################
# CRONJOBS
############################

kubectl get cronjobs
kubectl describe cronjob <cronjob>
kubectl create cronjob hello --image=busybox --schedule="*/1 * * * *"
kubectl delete cronjob <cronjob>

############################
# SERVICES
############################

kubectl get svc
kubectl get svc -A
kubectl describe svc <svc>
kubectl expose deployment nginx --port=80
kubectl delete svc <svc>

############################
# ENDPOINTS
############################

kubectl get ep
kubectl describe ep <ep>

############################
# INGRESS
############################

kubectl get ingress
kubectl get ingress -A
kubectl describe ingress <ingress>
kubectl delete ingress <ingress>

############################
# CONFIGMAPS
############################

kubectl get cm
kubectl describe cm <cm>
kubectl create cm app-config --from-file=config.properties
kubectl create cm app-config --from-literal=env=dev
kubectl delete cm app-config

############################
# SECRETS
############################

kubectl get secrets
kubectl describe secret <secret>
kubectl create secret generic mysecret --from-literal=user=admin
kubectl create secret tls tls-secret --cert=tls.crt --key=tls.key
kubectl delete secret mysecret

############################
# STORAGE
############################

kubectl get pv
kubectl get pvc
kubectl get sc
kubectl describe pv <pv>
kubectl describe pvc <pvc>
kubectl describe sc <sc>
kubectl delete pvc <pvc>
kubectl delete pv <pv>

############################
# SERVICE ACCOUNTS
############################

kubectl get sa
kubectl describe sa default
kubectl create sa app-sa
kubectl delete sa app-sa

############################
# RBAC
############################

kubectl get roles
kubectl get rolebindings
kubectl get clusterroles
kubectl get clusterrolebindings
kubectl describe role <role>
kubectl describe clusterrole <clusterrole>
kubectl auth can-i create pods
kubectl auth can-i --list

############################
# NETWORK POLICIES
############################

kubectl get networkpolicy
kubectl describe networkpolicy <policy>

############################
# RESOURCE QUOTA
############################

kubectl get quota
kubectl describe quota

############################
# LIMIT RANGE
############################

kubectl get limitrange
kubectl describe limitrange

############################
# EVENTS
############################

kubectl get events
kubectl get events -A
kubectl get events --sort-by=.metadata.creationTimestamp

############################
# METRICS
############################

kubectl top nodes
kubectl top pods
kubectl top pods -A
kubectl top pod <pod>

############################
# DEBUGGING
############################

kubectl describe pod <pod>
kubectl logs <pod>
kubectl logs -f <pod>
kubectl logs --previous <pod>
kubectl exec -it <pod> -- sh
kubectl debug node/<node>
kubectl debug pod/<pod>
kubectl get events
kubectl get events -A

############################
# LABELS
############################

kubectl label pod <pod> env=prod
kubectl label node <node> env=prod
kubectl get pods -l env=prod
kubectl get all -l env=prod

############################
# ANNOTATIONS
############################

kubectl annotate pod <pod> owner=devops
kubectl get pod <pod> --show-managed-fields

############################
# SELECTORS
############################

kubectl get pods -l app=nginx
kubectl get pods -l app!=nginx
kubectl get pods -l 'env in (prod,dev)'
kubectl get pods -l 'env notin (prod)'

############################
# OUTPUT FORMATS
############################

kubectl get pods -o wide
kubectl get pods -o yaml
kubectl get pods -o json
kubectl get pods -o name
kubectl get pods -o custom-columns=NAME:.metadata.name
kubectl get pods -o jsonpath='{.items[*].metadata.name}'

############################
# ALL RESOURCES
############################

kubectl get all
kubectl get all -A

############################
# MANIFEST OPERATIONS
############################

kubectl apply -f file.yaml
kubectl create -f file.yaml
kubectl replace -f file.yaml
kubectl delete -f file.yaml
kubectl diff -f file.yaml
kubectl kustomize .
kubectl apply -k .

############################
# API EXPLORATION
############################

kubectl explain pod
kubectl explain pod.spec
kubectl explain deployment.spec.template.spec

############################
# ETCD (CONTROL PLANE NODE)
############################

ETCDCTL_API=3 etcdctl endpoint health
ETCDCTL_API=3 etcdctl endpoint status
ETCDCTL_API=3 etcdctl member list
ETCDCTL_API=3 etcdctl snapshot save backup.db
ETCDCTL_API=3 etcdctl snapshot status backup.db

############################
# KUBEADM
############################

kubeadm version
kubeadm config view
kubeadm token list
kubeadm certs check-expiration
kubeadm certs renew all
kubeadm upgrade plan
kubeadm upgrade apply v1.xx.x
kubeadm reset

############################
# COMPONENT VERSIONS
############################

kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.kubeletVersion}'
kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.kubeProxyVersion}'
kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.containerRuntimeVersion}'
kubectl get pods -n kube-system -o wide
kubectl get componentstatuses

############################
# CERTIFICATES
############################

kubectl get csr
kubectl certificate approve <csr>
kubectl certificate deny <csr>
kubectl delete csr <csr>

############################
# CRD
############################

kubectl get crd
kubectl describe crd <crd>
kubectl api-resources

############################
# LEASES
############################

kubectl get leases -A

############################
# WEBHOOKS
############################

kubectl get validatingwebhookconfigurations
kubectl get mutatingwebhookconfigurations

############################
# API SERVER RAW CALLS
############################

kubectl get --raw='/healthz'
kubectl get --raw='/livez'
kubectl get --raw='/readyz'
kubectl get --raw='/metrics'
kubectl get --raw='/version'

############################
# ADVANCED JSONPATH
############################

kubectl get pods -A -o jsonpath='{.items[*].metadata.name}'
kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}'
kubectl get pods -o custom-columns=NAME:.metadata.name,IP:.status.podIP

############################
# ADVANCED CLUSTER AUDIT
############################

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

############################
# EVERYTHING IN CLUSTER
############################

kubectl api-resources --verbs=list --namespaced -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found -A

kubectl api-resources --verbs=list --namespaced=false -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found

################################################################################
# END OF CLUSTER ADMIN COMMANDS
################################################################################
