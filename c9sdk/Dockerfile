FROM ubuntu:16.04

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install curl git python -y

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install nodejs build-essential -y

RUN git clone git://github.com/c9/core.git c9sdk
WORKDIR c9sdk
RUN scripts/install-sdk.sh

RUN mkdir /workspace

EXPOSE 3000

CMD node server.js --port 3000 --auth account:password --listen 0.0.0.0 -w /workspace
