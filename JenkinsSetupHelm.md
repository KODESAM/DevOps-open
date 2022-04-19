## Jenkins server setup with Helm to deploy into Kubernetes cluster

Download and Install helm
```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh

```
Test with helm command
```
helm version
helm list

```
Copy config file from Kubernetes Cluster to Jenkins home directory
```
cd .kube
cp config
mkdir /var/lib/jenkins/.kube
copy config file under .kube directory with jenkins ownership
```
