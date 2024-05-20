# Use a specific version of Python image to ensure consistency across builds
FROM --platform=linux/amd64 ubuntu:22.04

ENV \
    DEBIAN_FRONTEND=noninteractive

# Copy library scripts to execute
COPY \
    library-scripts/*.sh library-scripts/*.env /tmp/library-scripts/

# Install Node.js, Azure Static Web Apps CLI and Azure Functions Core Tools
ARG NODE_VERSION="18"
ARG NPM_VERSION="10"
ARG CORE_TOOLS_VERSION="4"
ARG USERNAME="gen-cv"
ARG SWA_CLI_VERSION
ENV NVM_DIR="/usr/local/share/nvm" \
    NVM_SYMLINK_CURRENT=true \
    USER_GID=1000 \
    PATH="${NVM_DIR}/current/bin:${PATH}"

RUN \
    useradd --shell /bin/bash --create-home $USERNAME \
    && mkdir -p /etc/sudoers.d \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

RUN \
    bash /tmp/library-scripts/node-debian.sh "${NVM_DIR}" "${NODE_VERSION}" "${USERNAME}" \
    && apt-get update && apt-get upgrade && apt-get install -y libgtk2.0-0 libgtk-3-0 libgbm-dev libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2 libxtst6 xauth xvfb libsecret-1-0 software-properties-common curl \
    && if [ $CORE_TOOLS_VERSION != "4" ]; then apt-get remove -y azure-functions-core-tools-4 && apt-get install -y "azure-functions-core-tools-${CORE_TOOLS_VERSION}"; fi \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN \
    python3 /tmp/library-scripts/get-pip.py

RUN \
    bash /tmp/library-scripts/install-odbc-18-ubuntu.sh

RUN \
    curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash \
    && export NVM_DIR="/usr/local/share/nvm" \
    && [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" \
    && [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
    
USER gen-cv
WORKDIR /home/gen-cv
CMD ["/bin/bash"]