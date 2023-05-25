FROM jenkins/jenkins:latest
USER root

RUN update-ca-certificates

RUN apt-get update
RUN apt-get install -y zip python python3-pip npm jq wget curl unzip iproute2

RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 0
RUN pip3 install python-hcl2 slackclient requests ipaddress hvac
RUN apt-get update && apt-get install -y wget
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN ./aws/install

USER jenkins

ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

COPY ./jenkins.yaml $JENKINS_HOME/casc_configs/jenkins.yaml
ENV CASC_JENKINS_CONFIG=$JENKINS_HOME/casc_configs

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt
