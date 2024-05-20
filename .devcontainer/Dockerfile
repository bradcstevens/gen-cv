# Use a specific version of Python image to ensure consistency across builds
FROM mcr.microsoft.com/devcontainers/base:ubuntu

RUN sudo apt-get update && sudo apt upgrade -y
RUN sudo apt install software-properties-common -y
# RUN sudo add-apt-repository ppa:deadsnakes/ppa
# RUN sudo apt install python3.11 -y
# RUN sudo apt install python3-pip
RUN python3 -m pip install --upgrade pip
# RUN curl -sS https://bootstrap.pypa.io/get-pip.py | python3.11
COPY ../avatar/install-odbc-18-ubuntu.sh /tmp/install-odbc-18-ubuntu.sh
RUN sudo chmod +x /tmp/install-odbc-18-ubuntu.sh
RUN sudo /tmp/install-odbc-18-ubuntu.sh