FROM php:8.0-fpm
ENV PHP_IDE_CONFIG="serverName=localhost"
RUN apt-get update && apt-get install -y libpq-dev && docker-php-ext-install pdo pdo_pgsql
RUN apt update \
    && apt install -y zlib1g-dev g++ git libicu-dev zip libzip-dev zip libpq-dev \
    && docker-php-ext-install intl opcache pdo pdo_mysql pdo_pgsql \
    && pecl install apcu xdebug \
    && docker-php-ext-enable apcu \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

WORKDIR /var/www/app_directory
RUN apt-get update && apt-get install -y gnupg2 supervisor
RUN #supervisorctl start test-supervisor:*

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install yarn -y

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony
RUN #curl -sL https://deb.nodesource.com/setup_14.x | bash \
#      && apt-get install -y nodejs
RUN curl -fsSL https://deb.nodesource.com/setup_17.x | bash - \
      && apt-get install -y nodejs
