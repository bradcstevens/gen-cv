FROM mcr.microsoft.com/devcontainers/python:3

# Install pip for Python 3
RUN python -m pip install --upgrade pip

# Install Node Version Manager and Set Paths
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
RUN export NVM_DIR="$HOME/.nvm"
RUN [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
RUN [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# Install Node 18 with Node Version Manager
RUN nvm install node 18

# Set Node version to 18 as default
RUN nvm use 18
RUN nvm alias default 18