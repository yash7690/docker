FROM php:8.1-fpm-buster

RUN echo "Acquire::http::Pipeline-Depth 0;" > /etc/apt/apt.conf.d/privet && echo "Acquire::http::No-Cache true;" >> /etc/apt/apt.conf.d/privet && echo "Acquire::BrokenProxy    true;" >> /etc/apt/apt.conf.d/privet

RUN apt-get update

RUN apt-get -qq install -y \
    apt-utils \
    git \
    curl \
    wget \
    unzip \
    vim \
    nano \
    libzip-dev \
    libmcrypt-dev \
    libicu-dev \
    libxml2-dev libxslt1-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    mariadb-client \
    mailutils \
    golang-go \
    && docker-php-ext-configure hash --with-mhash \
    && docker-php-ext-configure gd --with-jpeg --with-freetype \
    && docker-php-ext-install intl zip xsl gd pdo_mysql opcache soap bcmath iconv pcntl sockets

RUN docker-php-ext-install mysqli

# Configuring php.ini
RUN apt-get install -y vim \
    && cd /usr/local/etc/php \
    && cp php.ini-development php.ini

# Memory Limit, Execution time and opcache settings - php.ini
RUN echo "memory_limit = 4G" > /usr/local/etc/php/conf.d/memory-limit.ini
RUN echo "max_execution_time = 1800" > /usr/local/etc/php/conf.d/max-execution-time.ini
RUN echo "opcache.enable = 1" > /usr/local/etc/php/conf.d/opcache.ini
RUN echo "opcache.save_comments = 1" > /usr/local/etc/php/conf.d/opcache.ini
RUN echo "upload_max_filesize = 1024M" > /usr/local/etc/php/conf.d/upload-max-size.ini

# Install Composer
RUN cd /usr/src && curl -sS http://getcomposer.org/installer | php
RUN cd /usr/src && mv composer.phar /usr/bin/composer
RUN composer config --global process-timeout 2000

# Install n98-magerun
RUN cd /usr/src && curl -O https://files.magerun.net/n98-magerun2.phar
RUN cd /usr/src && chmod +x ./n98-magerun2.phar && mv n98-magerun2.phar /usr/bin/magerun


#install ohmyposh
RUN wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O /usr/local/bin/oh-my-posh
RUN chmod +x /usr/local/bin/oh-my-posh

RUN mkdir ~/.poshthemes
RUN wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/themes.zip -O ~/.poshthemes/themes.zip
RUN unzip ~/.poshthemes/themes.zip -d ~/.poshthemes
RUN chmod u+rw ~/.poshthemes/*.json
RUN rm ~/.poshthemes/themes.zip
RUN echo 'eval "$(oh-my-posh init bash --config ~/.poshthemes/microverse-power.omp.json)"' > ~/.bashrc