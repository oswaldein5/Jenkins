# Practice-05 - Pipeline Test/Build/Merge/Create and upload Docker images from Jenkins 

## Go to Jenkins
- Install Plugin `CloudBees Docker Build and Publish`
- [Re]Configure Pipeline the same item `pipeline_CI_test`
----- *** All steps for App-Back
- Add `Add build step` select option `Docker Build and Publish` 
- Repository Name `repo/billingapp-back`
- Tag `0.0.1`
- Docker Host URI `tcp://host.docker.internal:2375` In this case for wsl2
- `curl http://localhost:2375/images/json`: Testing
- Docker registry URL `__` blank default use `https://hub.docker.com/`
- Enter credentials of Docker Hub
- In `Advanced` go to `Build Context` enter `Practice-05/billing/`: Repo Directory Context 
- In `Advanced` go to `Additional Build Arguments` enter `--build-arg  JAR_FILE=target/*.jar`
- Apply and Save
----- *** All steps for App-Front
 

