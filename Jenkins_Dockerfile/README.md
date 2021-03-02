https://linuxhint.com/install_jenkins_docker_ubuntu/
https://chathura-siriwardhana.medium.com/step-by-step-guide-to-add-jenkins-slave-nodes-f2e756c8849e >> SSH
https://www.edureka.co/community/48364/windows-slave-agent-jnlp-have-jenkins-master-configured-linux >> JNLP





In our case, Go to Manage Jenkins -> Configure Global Security -> under Agents section -> TCP port for inbound agents -> choose a custom Port (Here I choose 44059) and use the same port to run Jenkins, 

Example:-
docker run -p 8080:8080 -p 50000:50000 -p 44059:44059 --name=jenkins-master-server --mount source=jenkins-log,target=/var/log/jenkins --mount source=jenkins-data,target=/var/jenkins_home -d myjenkins
