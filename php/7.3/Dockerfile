FROM php:7.3

RUN apt-get clean && \
    apt-get update -qq && \
    apt-get install -y -qq \
        g++ \
        git \
        imagemagick \
        libicu-dev \
        libmagickwand-dev \
        libxml2-dev \
        libzip-dev \
        locales \
        openssh-client \
        rsync \
        unzip \
        zlib1g-dev && \
    rm -rf /var/lib/apt/lists/*

RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    echo "nl_NL.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen

RUN docker-php-ext-install bcmath && \
    docker-php-ext-install calendar && \
    docker-php-ext-install soap && \
    docker-php-ext-install zip && \
    docker-php-ext-install sockets && \
    docker-php-ext-install pdo pdo_mysql && \
    docker-php-ext-configure intl && docker-php-ext-install intl && \
    pecl install imagick && docker-php-ext-enable imagick && \
    pecl install pcov && docker-php-ext-enable pcov

RUN echo "date.timezone = Europe/Amsterdam" > /usr/local/etc/php/conf.d/timezone.ini && \
    echo "short_open_tag = off" > /usr/local/etc/php/conf.d/short_open.ini

RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php && \
    php composer-setup.php --1 --install-dir=/usr/local/bin/ --filename=composer1 && \
    php composer-setup.php --2 --install-dir=/usr/local/bin/ --filename=composer2 && \
    ln -s /usr/local/bin/composer1 /usr/local/bin/composer && \
    php -r "unlink('composer-setup.php');"

CMD ["php", "-a"]
