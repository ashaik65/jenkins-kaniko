

- https://blog.devstream.io/posts/devsecops-jenkins-in-k8s-with-secret-scan/

- https://github.com/GoogleContainerTools/kaniko



##### Terraform EKS
- https://github.com/quickbooks2018/terraform-aws-eks


##### Jenkins Setup on GCP GKE Cluster
```jenkins-gke
helm repo add jenkinsci https://charts.jenkins.io
helm repo update
helm install jenkins --namespace jenkins --create-namespace jenkinsci/jenkins


# Set up port forwarding to the Jenkins UI from Cloud Shell
kubectl -n jenkins port-forward svc/jenkins --address 0.0.0.0 8090:8080

# Jenkins Secrets

kubectl get secrets -n jenkins 

kubectl get secrets/jenkins -n jenkins -o yaml

jenkins-admin-password: b1NuY1NpWmdnR25ZemtuNWx5Mnl0NQ==
jenkins-admin-user: YWRtaW4=

echo -n 'b1NuY1NpWmdnR25ZemtuNWx5Mnl0NQ==' | base64 -d
oSncSiZggGnYzkn5ly2yt5
```



### Jenkins Commands

##### k8 credentials
```k8-secrets
kubectl create secret docker-registry docker-credentials --docker-username=[userid] --docker-password=[Docker Hub access token] --docker-email=[user email address] --namespace jenkins
```


### Jenkins Service Account
```k8-secrets
kubectl create serviceaccount jenkins --namespace=jenkins
kubectl describe secret $(kubectl describe serviceaccount jenkins --namespace=jenkins | grep Token | awk '{print $2}') --namespace=jenkins
kubectl create rolebinding jenkins-admin-binding --clusterrole=admin --serviceaccount=jenkins:jenkins --namespace=jenkins
kubectl get serviceaccounts -n jenkins
```
- Note: jenkins:jenkins serviceaccount:namespace


##### Jenkins Kaniko CI & HELM CD Pipe
```jenkins-pipe
kubectl create ns hello
kubectl create rolebinding jenkins-admin-binding --clusterrole=admin --serviceaccount=jenkins:default --namespace=hello
```


##### HELM CD deployment to AWS EKS
```
export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
export AWS_DEFAULT_REGION=us-west-2
```
