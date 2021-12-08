FROM php:8.0-fpm-bullseye
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

# timezone environment
ENV TZ=UTC \
  # locale
  LANG=en_US.UTF-8 \
  LANGUAGE=en_US:en \
  LC_ALL=en_US.UTF-8 \
  # composer environment
  COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

# ENV LIBRDKAFKA_VERSION v0.11.0
ENV BUILD_DEPS \
        build-essential \
        git \
        libsasl2-dev \
        libssl-dev \
        python \
        zlib1g-dev

COPY --from=composer:2.1 /usr/bin/composer /usr/bin/composer

RUN apt-get update && \
  apt-get -y install git libicu-dev libonig-dev libzip-dev unzip locales && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  locale-gen en_US.UTF-8 && \
  localedef -f UTF-8 -i en_US en_US.UTF-8 && \
  mkdir /var/run/php-fpm && \
  docker-php-ext-install intl pdo_mysql zip bcmath && \
  composer config -g process-timeout 3600 && \
  composer config -g repos.packagist composer https://packagist.org

RUN apt-get update \
    && apt-get install -y --no-install-recommends ${BUILD_DEPS} \
    && cd /tmp \
    && git clone \
        https://github.com/edenhill/librdkafka.git \
    && cd librdkafka \
    && ./configure \
    && make \
    && make install \
    && pecl install rdkafka \
    && docker-php-ext-enable rdkafka \
    && rm -rf /tmp/librdkafka \
    && apt-get purge \
        -y --auto-remove \
        -o APT::AutoRemove::RecommendsImportant=false \
        ${BUILD_DEPS}


COPY ./infra/docker/php/php-fpm.d/zzz-www.conf /usr/local/etc/php-fpm.d/zzz-www.conf
COPY ./infra/docker/php/php.ini /usr/local/etc/php/php.ini

WORKDIR /work/backend
