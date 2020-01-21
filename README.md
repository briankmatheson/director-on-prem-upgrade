# director-on-prem-upgrade: Rancher

## 0. Clone the chart
      ```
      git clone https://github.com/mayadata-io/director-charts.git
      ```
## 1. CD to appropriate (new) version
      e.g. upgrading from 1.5.0 to 1.6.0:
      cd director-charts/1.6.0
      ```

## 2. Remove ingress dependency
      ```
      rm -rf templates/{cm-nginx-configuration.yaml,clr-nginx-ingress-clusterrole.yaml,cm-tcp-services-ingress.yaml,cm-udp-services-ingress.yaml,crb-nginx-ingress-clusterrole-nisa-binding.yaml,dep-nginx-ingress-controller.yaml,ns-ingress-nginx.yaml,rlb-nginx-ingress-role-nisa-binding.yaml,role-nginx-ingress-role.yaml,sa-nginx-ingress-serviceaccount.yaml,svc-ingress-nginx.yaml,dep-default-http-backend.yaml,svc-default-http-backend}

## 3. Create (or use existing) docker secret for MayaData registry
      ```
      kubectl create ns <custom_namespace>
      kubectl create secret docker-registry <secretname> --docker-server=registry.mayadata.io --docker-username=<username> --docker-password=<password> -n <custom_namespace>
      ```
      Where <secretname> is the name of the secret to add (typically "directoronprem-registry-secret")
            <username> is the email address you used to sign up, as referenced in the Director On-Prem email
            <password> is the password included in that email
            <custom_namespace> is a unique namespace to install in (typically "director")
      ```
## 4. Edit values.yaml and apply changes to the file as needed (see sample in this repository)
### 4.1. Change dockerSecret name as necessary
### 4.2. Specify endpoint URL (typically address of nodeport or external Load Balancer endpoint)

## 5. Run helm install to install the local chart
      ```
      helm install directoronprem --namespace director .
      ```


## References:
* https://help.mayadata.io/hc/en-us/articles/360037922872-Setting-up-OpenEBS-Director-OnPrem-on-a-Rancher-based-kubernetes-cluster
