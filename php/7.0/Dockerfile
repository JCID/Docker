FROM php:7.0

# Container uitbreidingen (nodig voor composer)
RUN apt-get clean && apt-get update -qq
RUN apt-get install -y -qq unzip git zlib1g-dev locales zlib1g-dev libicu-dev g++
RUN rm -rf /var/lib/apt/lists/*

# Install dutch locale
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "nl_NL.UTF-8 UTF-8" >> /etc/locale.gen
RUN locale-gen

# PHP uitbreidingen
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install zip
RUN docker-php-ext-install calendar
RUN docker-php-ext-configure intl && docker-php-ext-install intl
RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN echo "date.timezone = Europe/Amsterdam" > /usr/local/etc/php/conf.d/timezone.ini
RUN echo "short_open_tag = off" > /usr/local/etc/php/conf.d/short_open.ini

# Installatie composer
RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer
RUN php -r "unlink('composer-setup.php');"

# Installatie afhankelijkheden
RUN composer global require "hirak/prestissimo:^0.3"

CMD ["php", "-a"]
