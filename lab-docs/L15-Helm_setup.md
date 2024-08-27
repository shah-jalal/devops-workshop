# Helm setup 

Prerequisites:
The following prerequisites are required for a successful and properly secured use of Helm.
A Kubernetes cluster:
- You must have Kubernetes
- You should also have a local configured copy of kubectl

1. Install helm from script
   ```sh 
   curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
   chmod 700 get_helm.sh
   ./get_helm.sh
   ```
1. Validate helm installation 
   ```sh
   helm version
   helm list
   ```
1. [optional] Download .kube/config file to build the node 
   ```sh
   aws eks update-kubeconfig --region us-east-1 --name ttrend-eks-cluster
   ```

1. Setup helm repo 
   ```sh 
   helm repo list
   helm repo add stable https://charts.helm.sh/stable
   helm repo update
   helm search repo <helm-chart>
   helm search repo stable
   ```

1. Install mysql charts on Kubernetes 
   ```sh 
   helm install demo-mysql stable/mysql 
   ```
1. To pull the package from repo to local 
   ```sh 
   helm pull stable/mysql 
   ```

  *Once you have downloaded the helm chart, it comes as a zip file. You should extract it.* 

  In this directory, you can find 
  - templates
  - values.yaml
  - README.md
  - Chart.yaml

  If you'd like to change the chart, please update your templates directory  and modify the version (1.6.9 to 1.7.0) in the chart.yaml

then you can run the command to pack it after your update
```sh
 helm package mysql
```

To deploy helm chart
```sh 
 helm install mysqldb mysql-1.6.9.tgz
```

Above command deploy MySQL 
To check deployment 
```sh 
 helm list 
```
To uninstall 
```sh 
 helm uninstall mysqldb
```

To install nginx 
```sh 
 helm repo search nginx 
 helm install demo-nginx stable/nginx-ingress
