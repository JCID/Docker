FROM php:7.1

# Container uitbreidingen (nodig voor composer)
RUN apt-get clean && apt-get update -qq > /dev/null 2>&1
RUN apt-get install -y -qq unzip git zlib1g-dev locales > /dev/null 2>&1
RUN rm -rf /var/lib/apt/lists/*

# Install dutch locale
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "nl_NL.UTF-8 UTF-8" >> /etc/locale.gen
RUN locale-gen > /dev/null 2>&1

# PHP uitbreidingen
RUN docker-php-ext-install bcmath > /dev/null 2>&1
RUN docker-php-ext-install zip > /dev/null 2>&1
RUN docker-php-ext-install calendar > /dev/null 2>&1
RUN pecl install xdebug > /dev/null 2>&1 && docker-php-ext-enable xdebug > /dev/null 2>&1
RUN echo "date.timezone = Europe/Amsterdam" > /usr/local/etc/php/conf.d/timezone.ini
RUN echo "short_open_tag = off" > /usr/local/etc/php/conf.d/short_open.ini

# Installatie composer
RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer
RUN php -r "unlink('composer-setup.php');"

# Installatie afhankelijkheden
RUN composer global require "hirak/prestissimo:^0.3"

CMD ["php", "-a"]
