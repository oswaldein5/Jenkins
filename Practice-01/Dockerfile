FROM jenkins/jenkins
# working with user root
USER root

# Update Base OS and install additional tools
RUN apt-get update && apt-get install -y maven

# returning to user jenkins
USER jenkins
