FROM rackspacedot/python37:latest

MAINTAINER Michael Kirk <michael.kirk@thomsonreuters.com>

ARG GH_RUNNER_VERSION="2.164.0"

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    curl \
    tar \
    zip \
    unzip

RUN pip install --upgrade pip && \
    pip install awscli

WORKDIR /actions-runner
COPY install_actions.sh /actions-runner

RUN chmod +x /actions-runner/install_actions.sh \
  && /actions-runner/install_actions.sh ${GH_RUNNER_VERSION} \
  && rm /actions-runner/install_actions.sh

WORKDIR /_work
COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]