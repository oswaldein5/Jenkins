# Practice-06 - 

## Go to Jenkins image Docker & install kubectl
- `docker exec -it --user=root jenkins /bin/bash`
- `curl -LO https://dl.k8s.io/release/v1.29.2/bin/linux/amd64/kubectl`
- `install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl`
- `kubectl version --client`

## Install Kubernetes plugin
`https://plugins.jenkins.io/kubernetes/`

## Go to local terminal
- `kubectl apply -f jenkins-account.yaml`: Create ServiceAccount w secret for jenkins
- `kubectl config view`
- `kubectl --namespace default get serviceaccount`
- `kubectl --namespace default get serviceaccount jenkins -o yaml`
- `kubectl describe secret jenkins` and copy token

## Go to Jenkins
- Go to `Dashboard > Manage Jenkins > Credentials > System>Global credentials (unrestricted)`
- Add credentials `Secret text` with copied token, in this case kubernetes-cluster
- Open the file `C:\Users\user\.kube\config`
- And copy certificate-authority-data for server: https://kubernetes.docker.internal:6443
- Go to `Dashboard > Manage Jenkins > Clouds`
- And enter name of Cloud, in this case Kubernetes
- Select option Type `Kubernetes`
- In `Kubernetes Cloud details`
- Kubernetes URL `https://kubernetes.docker.internal:6443`
- Kubernetes server certificate key certificate-authority-data from `C:\Users\user\.kube\config` in this case for wsl2
- Choose credentials, in this case `kubernetes-cluster`
- Check `Test Connection`
- Save
- Go to `+ New Item`
- Create new view `Deploy_K8s` as `pipeline`
- Check the option `GitHub project` and enter url repo github in `Project url` 
- In this case `https://github.com/oswaldein5/Jenkins/`
- In `Pipeline` choose `Pipeline script from SCM`
- In `Repositories/Repository URL` enter `https://[token|secrettext]@github.com/oswaldein5/Jenkins/`
- In `Branch Specifier (blank for 'any')` enter `main`
- In `Script Path` enter the path `Practice-06/Jenkinsfile`
- Execute `Deploy_K8s`
- Finally add this pipeline `Deploy_K8s` as `Build other projects` to the end of the job `pipeline_CI_test`
- Execute `pipeline_CI_test`


















- Install Plugin `CloudBees Docker Build and Publish`
- Go to `Dashboard > Manage Jenkins > Tools > Docker installations` then:
	- In`Name` enter name of installation
	- Check `Install automatically` and `Docker version` must be `latest`
- [Re]Configure Pipeline the same item `pipeline_CI_test`
----- *** All steps for App-Back
- Add `Add build step` select option `Docker Build and Publish` 
- Repository Name `repo/billingapp-back`
- Tag `0.0.1`
- Docker Host URI `tcp://host.docker.internal:2375` In this case for wsl2
- `curl http://localhost:2375/images/json`: Testing
- Docker registry URL `__` blank default use `https://hub.docker.com/`
- Enter credentials of Docker Hub
- In `Advanced`:
	- Go to `Build Context` enter `Practice-05/billing/`: Repo Directory Context 
	- Go to `Additional Build Arguments` enter `--build-arg  JAR_FILE=target/*.jar`
	- Go to `Docker installation` choose name of preview installation 
- Apply and Save
