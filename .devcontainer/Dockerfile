ARG VARIANT="ubuntu-20.04"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

# Metadata
LABEL org.opencontainers.image.source=https://github.com/stevethomas15977/custom-vscode-devcontainer
LABEL org.opencontainers.image.description="Dev tools (Ubuntu)"

# Install additional OS packages
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive && apt-get -y install --no-install-recommends

RUN apt-get -y install python3-pip
RUN apt-get -y install curl unzip
RUN pip3 install -q awscli-local localstack

RUN mkdir -p /var/lib/localstack
RUN chown vscode:vscode /var/lib/localstack

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN ./aws/install
RUN rm -rf aws*

RUN alias awslocal="AWS_ACCESS_KEY_ID=test AWS_SECRET_ACCESS_KEY=test AWS_DEFAULT_REGION=${DEFAULT_REGION:-$AWS_DEFAULT_REGION} aws --endpoint-url=http://${LOCALSTACK_HOST:-localhost}:4566"
