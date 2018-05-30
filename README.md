# spark-on-kubernetes-test
```
# minikube set config memory 8192
# minikube set config cpus 4
# minikube start 

$ eval $(sudo minikube docker-env)
# docker build -t spark:latest -f kubernetes/dockerfiles/spark/Dockerfile .

# kubectl create serviceaccount spark-role
# kubectl create rolebinding spark-role-edit-binding --clusterrole=edit --serviceaccount=default:spark-role --namespace=default

$ bin/spark-submit --master k8s://https://192.168.99.100:8443 --deploy-mode cluster --name spark-pi --class org.apache.spark.examples.SparkPi --conf spark.executor.instances=1 --conf spark.kubernetes.authenticate.driver.serviceAccountName=spark-role --conf spark.kubernetes.container.image=spark:latest local:///opt/spark/examples/jars/spark-examples_2.11-2.3.0.jar

# kubectl get pods -l spark-role=driver
# kubectl logs <pod-name>
```

https://github.com/kubernetes/minikube
https://spark.apache.org/docs/latest/running-on-kubernetes.html#rbac
https://kubernetes.io/docs/reference/access-authn-authz/rbac/
