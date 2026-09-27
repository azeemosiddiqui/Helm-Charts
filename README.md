# Helm-Charts
#Install HELM on AWS CLOUDSHELL:
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

helm version

# ADD HELM REPO (in below we added bitnami but it can be others also)
helm repo add <Repo Name>  https://<REPO URL>
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo add argo https://argoproj.github.io/argo-helm

# Install Argo CD with Image Updater enabled
kubectl create namespace argocd
helm repo add argo https://argoproj.github.io/argo-helm
helm install argocd argo/argo-cd --namespace argocd --set imageUpdater.enabled=true

# Helm Repo Update commands
helm repo update #UPDATE ALL REPO
helm repo update bitnami #UPDATE SINGLE REPO
helm search repo bitnami  #SEARCH CHART IN REPO
helm repo list   #LIST ALL HELM REPOS YOU HAVE INSTALLED


[k8s: eks-cluster-azeem] ~ $ helm repo list
NAME                                       URL                                               
bitnami                               https://charts.bitnami.com/bitnami                
ingress-nginx                     https://kubernetes.github.io/ingress-nginx        
prometheus-community     https://prometheus-community.github.io/helm-charts

# Install Application
helm install <release (any name we can give)> <repo-name/chart-name>
helm install my-nginx bitnami/nginx

# Uninstall Application
helm unistall <release (any name we can give)>
helm uninstall my-nginx

# To see what is already deployed
helm list
root@controlplane:~$ helm list                        
NAME      NAMESPACE       REVISION        UPDATED                                                   STATUS                   CHART             APP VERSION
az-redis        default         1               2026-06-28 04:55:10.911618078 +0000 UTC deployed        redis-27.0.12   8.8.0      
az-solr         default         1               2026-06-28 04:54:35.126437302 +0000 UTC deployed        solr-9.6.10     9.9.0     

# NOTE:When you run helm install, Helm deploys the pre-packaged application directly into your Kubernetes cluster as running containers. It does not download the source code or local copies of the Helm charts to your current working directory. 

helm pull bitnami/nginx --untar

# INSPECT THE CHART WITHOUT DOWNLOADING IT:
1- To view the default configuration options (values.yaml): 
helm show values bitnami/nginx

2- To view general information about the chart:
helm show chart bitnami/nginx

3- To view the README documentation:
helm show readme bitnami/nginx
