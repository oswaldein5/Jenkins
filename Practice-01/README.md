# Jenkins - Practice-01 

## Install Jenkins using Docker image & Dockerfile
## Dockerfile with instructions for installing Maven

- `docker build -t jenkins-mvn --no-cache .`: Build jenkins image using Dockerfile
- `docker run -d -p 8080:8080 -p 50000:50000 --name jenkins jenkins-mvn`: Create container jenkins
- `docker logs jenkins` : Check logs for password admin, this may also be found at: /var/jenkins_home/secrets/initialAdminPassword
- Go to http://localhost:8080 : console admin for jenkins