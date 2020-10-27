FROM jcid/php:7.4

RUN apt-get update && \
    apt-get install software-properties-common -y && \
    apt-get install -y -qq \
        curl \
        wget \
        libfontconfig1 \
        fontconfig \
        libxrender-dev \
        libfreetype6 \
        libxrender1 \
        zlib1g-dev \
        xvfb && \
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
    apt install -y ./google-chrome-stable_current_amd64.deb && \
    rm -rf ./google-chrome-stable_current_amd64.deb && \
    rm -rf /var/lib/apt/lists/*

RUN latest=$(curl -s https://chromedriver.storage.googleapis.com/LATEST_RELEASE) && \
    curl -s https://chromedriver.storage.googleapis.com/${latest}/chromedriver_linux64.zip -O && \
    unzip -q -o chromedriver_linux64.zip && \
    mv chromedriver /usr/bin/chromedriver && \
    rm chromedriver_linux64.zip

ENV PANTHER_CHROME_DRIVER_BINARY=/usr/bin/chromedriver
ENV PANTHER_NO_SANDBOX=1
ENV PANTHER_WEB_SERVER_PORT=9080

CMD ["php", "-a"]
