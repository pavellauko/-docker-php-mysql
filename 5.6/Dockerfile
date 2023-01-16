FROM vanio/php-mysql:5.6
RUN a2enmod headers
RUN apt-get update && apt-get install -y \
    vim \
    wget \
    curl \
    openssl \
    libssl-dev \
    zip \
    unzip \
    zlib1g-dev \
    libzip-dev \
    libmcrypt-dev \
    libwebp-dev \
    libsqlite3-dev \
    libsqlite3-0 \
    mysql-client \
    sendmail

# composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# sendmail
RUN echo "sendmail_path=/usr/sbin/sendmail -t -i" >> /usr/local/etc/php/conf.d/sendmail.ini
RUN sed -i '/#!\/bin\/sh/aservice sendmail restart' /usr/local/bin/docker-php-entrypoint
RUN sed -i '/#!\/bin\/sh/aecho "$(hostname -i)\t$(hostname) $(hostname).localhost" >> /etc/hosts' /usr/local/bin/docker-php-entrypoint

# php libs
RUN docker-php-ext-install iconv bcmath mbstring zip && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install mysqli && \
    docker-php-ext-enable mysqli

# cleaning
RUN apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*
