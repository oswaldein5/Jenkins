# Practice-05 - Upload billingapp-back:0.0.1 from Jenkins to Docker Hub 

## Go to Jenkins
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
