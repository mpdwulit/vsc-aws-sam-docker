FROM tensorflow/tensorflow:latest-gpu

LABEL maintainer Marek Dwulit<Marek.Dwulit@agilebeat.com>”

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get -y install sudo vim mc git wget gcc g++ python3.8
RUN apt-get -y install gnome-terminal --fix-missing
RUN apt-get -y install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

# Install Docker CE CLI
RUN apt-get update \
    && apt-get install -y apt-transport-https ca-certificates curl gnupg2 lsb-release \
    && curl -fsSL https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]')/gpg | apt-key add - 2>/dev/null \
    && echo "deb [arch=amd64] https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]') $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list \
    && apt-get update \
    && apt-get install -y docker-ce-cli

# Install Docker Compose
RUN LATEST_COMPOSE_VERSION=$(curl -sSL "https://api.github.com/repos/docker/compose/releases/latest" | grep -o -P '(?<="tag_name": ").+(?=")') \
    && curl -sSL "https://github.com/docker/compose/releases/download/${LATEST_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose

# RUN pip install pyinquirer --upgrade
RUN pip install --upgrade numpy
RUN pip --no-cache-dir install awscli opencv-python Pillow tensorflowjs

# https://deb.nodesource.com/setup_12.x is a bash script that prepares for installing NodeJS
RUN curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash - && sudo apt-get install -y nodejs

RUN npm install -g serverless
RUN npm install -g serverless-apigw-binary
RUN npm install -g serverless-apigwy-binary
RUN npm install -g npm@latest
RUN npm config set unsafe-perm=true

RUN pip install --upgrade pip
RUN pip install pylint numpy pandas geopandas matplotlib rope importlib_resources autopep8 geopy boto3
RUN pip install boto3  awscli aws-sam-cli
RUN /usr/bin/python3 -m pip install --upgrade pip