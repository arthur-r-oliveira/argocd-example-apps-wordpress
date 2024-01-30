# argocd-example-apps-wordpress

Sample stateful deployment with Persistent Volume, based on k8s sample https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume, but adapted (SCCs/ClusterRoleBinding/ServiceAccount/Routes) for OpenShif. Wordpress front end requires anyuid SCC on OpenShift. 

~~~
arolivei@arolivei-thinkpadp1gen3:~/utils/code/argocd-example-apps-wordpress$ kubectl apply -k ./
namespace/example-apps-wordpress unchanged
serviceaccount/example-apps-wordpress unchanged
clusterrolebinding.rbac.authorization.k8s.io/system:openshift:scc:anyuid unchanged
secret/mysql-pass-tmbk2k5m9f unchanged
service/wordpress unchanged
service/wordpress-mysql unchanged
persistentvolumeclaim/mysql-pv-claim unchanged
persistentvolumeclaim/wp-pv-claim unchanged
deployment.apps/wordpress unchanged
deployment.apps/wordpress-mysql unchanged
route.route.openshift.io/example-apps-wordpress unchanged
arolivei@arolivei-thinkpadp1gen3:~/utils/code/argocd-example-apps-wordpress$ oc get pods -o wide
NAME                               READY   STATUS    RESTARTS   AGE     IP             NODE                                  NOMINATED NODE   READINESS GATES
wordpress-64986c594f-gpdk4         1/1     Running   0          9m52s   10.128.0.222   arolivei-app-sno.example.com   <none>           <none>
wordpress-mysql-6bcf55dfc7-wgrd4   1/1     Running   0          26m     10.128.0.210   arolivei-app-sno.example.com   <none>           <none>
arolivei@arolivei-thinkpadp1gen3:~/utils/code/argocd-example-apps-wordpress$ oc get svc
NAME              TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
wordpress         ClusterIP   172.30.181.223   <none>        80/TCP     26m
wordpress-mysql   ClusterIP   None             <none>        3306/TCP   26m
arolivei@arolivei-thinkpadp1gen3:~/utils/code/argocd-example-apps-wordpress$ oc get routes
NAME                     HOST/PORT                                                         PATH   SERVICES    PORT   TERMINATION   WILDCARD
example-apps-wordpress   example-apps-wordpress.apps.arolivei-app-sno.example.com          wordpress   80                   None
arolivei@arolivei-thinkpadp1gen3:~/utils/code/argocd-example-apps-wordpress$ curl -k -I example-apps-wordpress.apps.arolivei-app-sno.example.com 
HTTP/1.1 200 OK
date: Tue, 30 Jan 2024 21:52:58 GMT
server: Apache/2.4.56 (Debian)
x-powered-by: PHP/8.0.28
link: <http://example-apps-wordpress.apps.arolivei-app-sno.example.com/wp-json/>; rel="https://api.w.org/"
content-type: text/html; charset=UTF-8
set-cookie: 0105d574202e7dbc5ee944c6f33165d5=32c45a047491f2acee5d5070e45f42bc; path=/; HttpOnly
cache-control: private
~~~ 
