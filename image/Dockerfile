### Dockerfile for docker slave (Go builder) on jenkins  Bohdan Pakhomov (10.03.20)###

FROM centos:centos7

MAINTAINER Bohdan Pakhomov <shtormless@gmail.com>

ENV TZ=Europe/Kiev

ARG VERSION=4.0.1
ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000

RUN groupadd -g ${gid} ${group}
RUN useradd -d /home/${user} -u ${uid} -g ${group} ${user}

ARG AGENT_WORKDIR=/home/${user}/agent

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    && yum update -y java-1.8.0-openjdk-devel wget git \
    && yum install -y java-1.8.0-openjdk-devel wget git \
    && curl --create-dirs -fsSLo /usr/share/jenkins/agent.jar https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/${VERSION}/remoting-${VERSION}.jar \
    && chmod 755 /usr/share/jenkins \
    && chmod 644 /usr/share/jenkins/agent.jar \
    && ln -sf /usr/share/jenkins/agent.jar /usr/share/jenkins/slave.jar \
    && wget https://dl.google.com/go/go1.14.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go1.14.linux-amd64.tar.gz \
    && export PATH=/go/bin:/usr/local/go/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    && yum clean all -y

ENV GOPATH=/go
ENV PATH=/go/bin:/usr/local/go/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

USER ${user}
ENV AGENT_WORKDIR=${AGENT_WORKDIR}
RUN mkdir /home/${user}/.jenkins && mkdir -p ${AGENT_WORKDIR}

VOLUME /home/${user}/.jenkins
VOLUME ${AGENT_WORKDIR}
WORKDIR /home/${user}
