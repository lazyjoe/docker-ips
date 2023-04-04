FROM php:7.4-fpm
ARG TIMEZONE

ENV ALIAS1="alias ll='ls -al --color=auto'"
ENV ALIAS2="alias hg='history|grep -v grep|grep -v hg|grep'"
ENV ALIAS3="alias pag='ps aux|grep -v grep|grep -v pag|grep'"

RUN echo "memory_limit=512M" > /usr/local/etc/php/conf.d/memory-limit.ini && \
    sed -i 's/;security.limit_extensions =.*/security.limit_extensions = .php .html .htm .txt .js .css .ico .woff .woff2 .png .ttf/g' /usr/local/etc/php-fpm.d/www.conf && \
    curl -sL https://deb.nodesource.com/setup_14.x | bash - && apt-get update && apt-get install -y \
    openssl \
    git \
    unzip \
    libpng-dev \
    python2 \
    nodejs && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-install pdo pdo_mysql gd mysqli && \
    ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone && \
    printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini && \
    pecl install xdebug-3.0.4 && \
    docker-php-ext-enable xdebug && \
    echo "$ALIAS1" >> ~/.bashrc && \
    echo "$ALIAS2" >> ~/.bashrc && \
    echo "$ALIAS3" >> ~/.bashrc && \
    echo "$ALIAS4" >> ~/.bashrc && \
    echo "$ALIAS5" >> ~/.bashrc && \
    echo "source ~/.bashrc" >> ~/.bash_profile && \
    rm -rf /var/lib/apt/lists/*

ENV XDEBUG_MODE=debug
ENV XDEBUG_CONFIG="remote_enable=1 remote_mode=req client_port=9001 client_host=host.docker.internal discover_client_host=0 idekey=VSCODE"

WORKDIR /var/www/forum