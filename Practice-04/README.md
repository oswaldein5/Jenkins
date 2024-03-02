# Practice-04 - Jenkins CI with Sonarqube

- `docker pull sonarqube`:
- `docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube`:
- `docker network create sonarq-jenkins`: 
- `docker network connect sonarq-jenkins sonarqube`: 
- `docker network connect sonarq-jenkins jenkins`: 
- `docker container inspect sonarqube`: 
- `docker container inspect jenkins`: 

## Go to Sonarqube
- Go to `http://localhost:9000`: Sonarqube Portal
- Go to Administration/Security/Users
- Add Tokens to user Administrator for Jenkins

## Go to Jenkins
- Install plugin SonarQube ScannerVersion
- Go to `Manage jenkins > System > SonarQube servers`
- Enter Name `sonarq_test` and Server URL `http://sonarqube:9000`
- Add credentials using generated token in Sonarqube
- Apply and Save
- Go to `Manage jenkins > configureTools > SonarQube Scanner installations`
- Enter Name: `sonarscanner`
- Apply and Save
- Go to `pipeline_CI_test`
- Go to `Build Steps` and choose the option `Execute SonarQube Scanner`
- In `Analysis properties` enter the following cmds:
	- sonar.projectKey=sonarqube
	- sonar.sources=Practice-04/billing/src/main/java
	- sonar.java.binaries=Practice-04/billing/target/classes
- In `Additional arguments` enter `-X`
- Apply and Save

## Go to Jenkins
- Check pipeline `pipeline_CI_test`
