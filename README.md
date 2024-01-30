# argocd-example-apps-wordpress

Sample stateful deployment with Persistent Volume, based on k8s sample https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume, but adapted (SCCs/ClusterRoleBinding/ServiceAccount/Routes) for OpenShif. Wordpress front end requires anyuid SCC on OpenShift. 
