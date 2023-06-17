FROM php:5.4-apache

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 04EE7237B7D453EC \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 648ACFD622F3D138 \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 0E98404D386FA1D9 \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EF0F382A1A7B6500 \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys AA8E81B4331F7F50 \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 112695A0E562B32A \
    && echo "deb http://archive.debian.org/debian/ stretch main" > /etc/apt/sources.list \
    && echo "deb http://archive.debian.org/debian-security stretch/updates main" >> /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y \
        git \
        zip \
        unzip \
        libxslt1-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install xsl

RUN pecl install apcu-4.0.11 && docker-php-ext-enable apcu

RUN a2enmod rewrite

ENV APACHE_DOCUMENT_ROOT /var/www/html/web
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

COPY php.ini /usr/local/etc/php
