ARG VARIANT=11-bullseye
FROM mcr.microsoft.com/devcontainers/java:1-${VARIANT}

SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

ARG APP_NAME
ENV APP_NAME=${APP_NAME:-myapp}

WORKDIR /workspaces/${APP_NAME}

ENV LANG=C.UTF-8 \
    TZ=Asia/Tokyo

# Install packages
RUN apt-get update -qq && export DEBIAN_FRONTEND=noninteractive && \
    # apt-get install --no-install-recommends -y \
    apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists /var/cache/apt/archives

# Create Maven repository
# RUN sudo -u vscode sh -c 'mkdir -p /home/vscode/.m2'
USER vscode
RUN mkdir -p /home/vscode/.m2 && \
    cat <<EOF > /home/vscode/.m2/settings.xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
  <localRepository>${PWD}/.m2/repository</localRepository>
</settings>
EOF

COPY . .
