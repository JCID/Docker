FROM ubuntu

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update --fix-missing \
    && apt-get -y upgrade \
    && apt-get install -y \
       apt-utils \
       curl \
       gnupg \
       openssh-client \
       sudo \
       unzip \
       wget

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add - \
    && sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list' \
    && curl -sSL https://deb.nodesource.com/setup_14.x | bash - \
    && apt-get update \
    && apt-get install -y google-chrome-stable nodejs

ARG CACHEBUST=1
RUN npm install --global lighthouse lighthouse-ci
