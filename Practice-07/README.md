# Practice-07 - Deploy Jenkins on a local kubernetes cluster using Helm

## Install K8s tools "kubectx" usefull for manage more than one context
- `https://github.com/ahmetb/kubectx`

## Create namespace in K8s for Jenkins
- `kubectl create namespace jenkins`
- `kubectl get namespaces`
- `kubens jenkins`: Move to namespace:jenkins
- ``

## Install Helm [In this case for Ubuntu]
- `sudo snap install helm --classic`

## Install Jenkins from Helm
- `helm repo add jenkins https://charts.jenkins.io`
- `helm repo update`
- `helm repo list`
- `helm show values jenkins/jenkins > values.yaml`: Get Chart default values
- `helm install jenkins jenkins/jenkins`
- `kubectl get pods`
- Follow the instructions:
	- `kubectl exec --namespace jenkins -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/additional/chart-admin-password && echo`: Get password
	- `kubectl --namespace jenkins port-forward svc/jenkins 8080:8080`: Access to jenkins:8080
- Go to http://localhost:8080/

## Deploy Jenkins from Chart:jenkins.values.yaml
- Modify jenkins.values.yaml adding more settings
- `helm install jenkins jenkins/jenkins -n jenkins -f jenkins.values.yaml`
- Follow the instructions:
	- `kubectl exec --namespace jenkins -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/additional/chart-admin-password && echo`: Get password
	- `kubectl --namespace jenkins port-forward svc/jenkins 8080:8080`: Access to jenkins:8080
- Go to http://localhost:8080/

