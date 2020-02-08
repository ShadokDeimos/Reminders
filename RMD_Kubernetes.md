# KUBERNETES

## INSTALLATION

### WITH CURL

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl

chmod +x ./kubectl

sudo mv ./kubectl /usr/local/bin/kubectl

kubectl version

```

### WITH Native package management

```
sudo apt-get update && sudo apt-get install -y apt-transport-https

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update

sudo apt-get install -y kubectl
```

### Install Minikube (to manager a K8S cluster on one single host)

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube

sudo mkdir -p /usr/local/bin/

sudo install minikube /usr/local/bin/

# Cleanup local state

minikube start

minikube delete			# if minikube start return "machine does not exist"
```

## Namespaces & Contexts

### Create namespace 

namespace.yaml 
```
{
  "apiVersion": "v1",
  "kind": "Namespace",
  "metadata": {
    "name": "development",
    "labels": {
      "name": "development"
    }
  }
}
```
```
kubectl create -f namespace.yaml

kubectl get namespaces --show-labels					Display all namespaces
```

```
kubectl config view								Display cluster and contexts informations 
kubectl config current-context					Display current context
kubectl config set-context preprod \ 			Create context in a namespace
	--namespace=preproduction \ 
	--cluster=minikube --user=minikube
kubectl config delete-context <context>			Delete specified context
```

## Services & Expose

```
kubectl port-forward <object-name> <public-port>:<container-port>
```

## K8S OBJECT (apiVersion)

CertificateSigningRequest		certificates.k8s.io/v1beta1
ClusterRoleBinding				rbac.authorization.k8s.io/v1
ClusterRole						rbac.authorization.k8s.io/v1
ComponentStatus					v1
ConfigMap						v1
ControllerRevision				apps/v1
CronJob							batch/v1beta1
DaemonSet						extensions/v1beta1
Deployment						extensions/v1beta1
Endpoints						v1
Event							v1
HorizontalPodAutoscaler			autoscaling/v1
Ingress							extensions/v1beta1
Job								batch/v1
LimitRange						v1
Namespace						v1
NetworkPolicy					extensions/v1beta1
Node							v1
PersistentVolumeClaim			v1
PersistentVolume				v1
PodDisruptionBudget				policy/v1beta1
Pod								v1
PodSecurityPolicy				extensions/v1beta1
PodTemplate						v1
ReplicaSet						extensions/v1beta1
ReplicationController			v1
ResourceQuota					v1
RoleBinding						rbac.authorization.k8s.io/v1
Role							rbac.authorization.k8s.io/v1
Secret							v1
ServiceAccount					v1
Service							v1
StatefulSet						apps/v1

## Examples

### PersistentVolume

pv-volume.yaml

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: ecd-file-pvclaim
  labels:
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```

pvclaim-volume.yaml

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: ecd-file-pvclaim
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi

```