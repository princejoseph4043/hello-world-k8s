FROM jenkins/jenkins
LABEL maintainer="princej@qburst.com"
USER root
RUN mkdir /var/log/jenkins
RUN mkdir /var/cache/jenkins
RUN chown -R jenkins:jenkins /var/log/jenkins
RUN chown -R jenkins:jenkins /var/cache/jenkins
RUN curl -LO https://github.com/argoproj/argo-cd/releases/download/v1.2.0/argocd-linux-amd64
RUN mv argocd-linux-amd64 /usr/local/bin/argocd
RUN chmod 755 /usr/local/bin/argocd
USER jenkins
 
ENV JAVA_OPTS="-Xmx8192m"
ENV JENKINS_OPTS="--handlerCountMax=300 --logfile=/var/log/jenkins/jenkins.log --webroot=/var/cache/jenkins/war"
