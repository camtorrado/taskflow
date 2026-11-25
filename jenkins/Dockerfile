FROM docker:cli AS docker-cli

FROM jenkins/jenkins:lts-jdk21

USER root

RUN apt-get update && apt-get install -y \
    python3 \
    python3-venv \
    python3-pip \
    git \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

COPY --from=docker-cli /usr/local/bin/docker /usr/local/bin/docker

COPY --from=docker-cli /usr/local/libexec/docker/cli-plugins/docker-compose /usr/local/lib/docker/cli-plugins/docker-compose

RUN chmod +x /usr/local/bin/docker \
    /usr/local/lib/docker/cli-plugins/docker-compose

USER jenkins
