FROM vanio/php-mysql:7.2
RUN a2enmod headers
RUN apt-get update && apt-get install -y \
    vim \
    wget \
    curl \
    zip \
    unzip \
    zlib1g-dev \
    libzip-dev \
    libmcrypt-dev \
    libwebp-dev \
    libicu-dev \
    sendmail

# composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# sendmail
RUN echo "sendmail_path=/usr/sbin/sendmail -t -i" >> /usr/local/etc/php/conf.d/sendmail.ini
RUN sed -i '/#!\/bin\/sh/aservice sendmail restart' /usr/local/bin/docker-php-entrypoint
RUN sed -i '/#!\/bin\/sh/aecho "$(hostname -i)\t$(hostname) $(hostname).localhost" >> /etc/hosts' /usr/local/bin/docker-php-entrypoint

# php libs
RUN docker-php-ext-install iconv bcmath zip && \
    pecl install mcrypt-1.0.4 && \
    docker-php-ext-enable mcrypt && \
    docker-php-ext-configure intl && \
    docker-php-ext-install intl

# cleaning
RUN rm -rf /var/lib/apt/lists/*
